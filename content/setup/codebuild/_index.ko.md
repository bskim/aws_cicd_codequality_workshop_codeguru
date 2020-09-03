---

title: "CodeBuild Report"
weight: 26
pre: "<b>2-5. </b>"

---


### **CodeBuild**의 보고서 기능을 추가할 것입니다.

실습에 사용할 코드는 Junit을 사용하여 유닛테스트를 수행합니다. 유닛테스트가 수행된 결과는 xml로 발행되고 개발자는 이것을 사용하여 본인의 코드가 어떤 유닛테스트를 통과하지 못했는지를 알 수 있어야합니다.  

Codebuild 콘솔로 가기: https://console.aws.amazon.com/codebuild

1. 오른쪽 Build텝의 **Report groups**를 선택합니다. 그리고 오른쪽 상단의 **Create report group**을 선택합니다.
    ![codebuild02](/images/codebuild-report.png)

1. Rport group configuration의 **Report group name**에 `Concurrency-Unittest-Report`를 입력합니다. **Export to Amazon S3**의 체크박스는 해제합니다.
    ![codebuild02](/images/cloudbuild-report-2.png)

1. 생성된 Report groups의 ARN을 복사하기위해  **Report groups**에서 **Concurrency-Unittest-Report**를 선택합니다. 
    ![codebuild02](/images/codebuild-report-arn.png)

1. 이제 이곳에 수행한 Unittest의 결과가 보여질 것입니다. Configuration의 **Report group ARN**의 내용을 복사합니다. 
    ![codebuild02](/images/codebuild-report-copy-arn.png)

1. 이제 **Cloud9**으로 돌아가 **buildspec.yml**을 수정하겠습니다. **buildspec.yml**은 ConcurrencySample의 루트디렉토리에 있습니다. 
    ![DataLakeStorage03](/images/cloudbuild-report-cloud9.png)
    파일을 더블클릭하여 내용을 추가합니다. `<YOUR-REPORT-GROUP-ARN>` 에 아까 복사한 **Report group ARN**을 붙여넣습니다.
    ```yml
    reports:
      <YOUR-REPORT-GROUP-ARN>:
        files:
          - '**/*'
        base-directory: 'build/test-results/test'
    ```

1. **buildspec.yml**의 최종 내용을 아래와 같습니다.
    ```yml
    version: 0.2
    
    phases:
      install:
        runtime-versions:
          java: corretto11
        commands:
          - java -version
          - gradle -version
      build:
        commands:
          - ./gradlew clean build
    reports:
      <YOUR-REPORT-GROUP-ARN>:
        files:
          - '**/*'
        base-directory: 'build/test-results/test'      
    artifacts:
      files:
        - '**/*'
      name: concurrencysample-$(date +%Y-%m-%d) 
    
    ```
1. 변경된 내용을 Commit한 뒤 push하여 반영하겠습니다. 
    ```bash
    cd ConcurrencySample
    git add .
    git commit -m "change Buildspec.yml"
    git push
    ```

1. 변경된 내용이 잘 반영되었는지 확인하겠습니다. 왼쪽 메뉴의 **Build**의 **Build projects**를 선택하여 **concurrencysample**를 선택합니다. 
    ![codebuild02](/images/codebuild-report-confirm.png)

1. 실패한 빌드를 확인할 수 있습니다. 내용을 눌러 확인해보겠습니다. 
    ![codebuild02](/images/codebuild-report-buildfail.png)
    아래 메세지를 보면 빌드 자체는 성공한 것을 볼 수 있습니다. 하지만 UnitTest가 실패한 것을 볼 수 있습니다. 
    ![codebuild02](/images/codebuild-report-unittestfail.png)
    이렇게 보면 어떤 테스트를 어떻게 통과했는지 자세한 내용을 보기 어렵기 때문에 build폴더에 생성된 report파일을 참조하거나 xml파일을 보실 수 있습니다. 하지만 이전에 연동한 CodeBuild Report를 이용하면 빌드 별 결과를 손쉽게 확인하실 수 있습니다.  
    **Report groups**로 가서 업로드된 report를 확인하겠습니다. 

1. 왼쪽 Build메뉴의 **Report groups**를 선택합니다. 그리고 아까 만든 **Cuncurrency-Unittest-Report**를 선택합니다. 
    ![codebuild02](/images/codebuild-report-show.png)

1. 성공실패와 수행시간을 그래프로 볼 수 있고 하단의 reports history의 report를 누르시면 UnitTest의 세부사항을 보실 수 있습니다. Console로 보는 것보다 훨씬 편하게 확인이 가능합니다.  
    ![codebuild02](/images/codebuild-report-graph.png)
    ![codebuild02](/images/codebuild-report-detail.png)
    ![codebuild02](/images/codebuild-report-detail2.png)

    

-[유닛테스트가 왜 실패했는지, 어떻게 수정해야하는지는 다음 프로그램 분석에서 하나씩 알아보겠습니다.](/ko/codequality/) 
