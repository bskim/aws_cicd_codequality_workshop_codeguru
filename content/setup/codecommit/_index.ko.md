---
title: "CodeCommit"
weight: 23
pre: "<b>2-2. </b>"

---

### 실습에 사용할 CodeCommit과 소스코드를 생성합니다. 
AWS CodeCommit은 안전한 Git 기반 리포지토리를 호스팅하는 완전관리형 소스 제어 서비스입니다. 이 서비스를 사용하면 뛰어난 확장성의 안전한 에코시스템에서 여러 팀이 협업하여 코드 작업을 수행할 수 있습니다. 실제 작업코드는 Github에 있기 때문에 이 코드를 사용자의 CodeCommit Repo로 옮기는 작업을 시작하겠습니다. 

1.	이제 Cloud9에서 실습에 사용할 코드를 셋팅할 것입니다. Cloud9의 Terminal에 아래와 같은 명령어를 입력합니다.

    ```bash
    git clone https://github.com/sykang169/ConcurrencySample.git
    ```

1. 위 명령어가 잘 실행되었다면 왼쪽 Environment이 파일창에 아래와 같이 concurrencysample이라는 폴더가 생성됩니다. 
    ![CodeCommit01](/images/codecommit-master.png)

1. 해당 repository의 기본 branch가 master기 때문에 clone은 master branch를 가져옵니다. 폴더의 내용을 살펴보면 README.md파일 외에는 별다른 파일이 없습니다.
실습에 필요한 진짜 소스코드는 develop에 있으니 develop Branch를 pull 합니다. 

    ```bash
    cd ConcurrencySample
    git checkout origin/develop -b develop
    ```

1. master보다 훨씬 많은 파일이 생성된것을 보실 수 있습니다. 이제 master와 develop의 코드들을 방금전 cloudformation에서 자동으로 생성한 codecommit의 **concurrencysample** repository로 변경할 것입니다. 	
    ![CodeCommit02](/images/codecommit-develop.png)


1.	CloudFormation의 Output을 확인하기위해 CloudFormation 콘솔로 갑니다. 

    CloudFormation 콘솔로 가기: https://console.aws.amazon.com/cloudformation/home
    
    또는 AWS 콘솔의 Services에서 Management & Governance의 **CloudFormation**을 선택합니다. 
    ![CodeCommit02](/images/codecommit-cloudformation.png)


1.	왼쪽 메뉴의 **Stacks**를 선택하고 방금 생성한 **CodeQuality-Workshop**을 선택합니다. 이곳에서 생성한 Stack의 디테일한 정보를 확인할 수 있습니다. 
    ![CodeCommit02](/images/codecommit-cloudformation-select-stack.png)

1.	Stack의 상세 내용에서 상단의 Outputs을 선택합니다. 거기서 우리가 진짜 repository로 사용할 CodeCommit의 URL을 **copy**합니다. 
    ![CodeCommit02](/images/codecommit-cloudformation-stacks-output.png)

1. 이제 다시 Cloud9으로 돌아갑니다. 이전에 생성한 concurrencysample폴더에서 현재 origin의 url을 확인합니다. 
    ```bash
    git remote show origin
    ```
    명령어를 입력하면 현재 설정된 origin의 url을 보여줍니다. 
    ```bash
    remote origin
    Fetch URL: https://github.com/sykang169/ConcurrencySample.git
    Push  URL: https://github.com/sykang169/ConcurrencySample.git
    HEAD branch: master
    Remote branches:
        develop tracked
        master  tracked
    Local branches configured for 'git pull':
        develop merges with remote develop
        master  merges with remote master
    Local refs configured for 'git push':
        develop pushes to develop (up to date)
        master  pushes to master  (up to date)
    ```
    origin의 url을 https://github.com/sykang169/ConcurrencySample.git에서 새로 생성한 codecommit의 주소로 변경합니다. 
  
    Cloud9의 터미널에 아래와 같이 입력하여 Git의 origin 주소를 변경합니다.**<YOUR_REPOSITORY-URL>**은 아까 CloudFormation의 Stack에서 복사한 CodeCommit의 URL정보입니다. 
    ```bash
    git remote set-url origin <YOUR-REPOSITORY-URL>
    ``` 
    명령어가 수행된 뒤 다시 `git remote show origin`으로 확인해보면 origin의 URL이 자신의 CodeCommit주소로 변경된 것을 확인할 수 있습니다. 
    ```bash
    Fetch URL: <YOUR_REPOSITORY-URL>
    Push  URL: <YOUR_REPOSITORY-URL>
    HEAD branch: master
    Remote branches:
        develop tracked
        master  tracked
    Local branches configured for 'git pull':
        develop merges with remote develop
        master  merges with remote master
    Local refs configured for 'git push':
        develop pushes to develop (up to date)
        master  pushes to master  (up to date)
    ```

1. 이제 변경된 CodeCommit Repository로 Cloud9의 코드를 Push하겠습니다. 먼저 master로 checkout한 후 push 합니다. CodeCommit의 Repo는 아직 한 건의 Push도 없기 때문에 먼저 생성된 브랜치가 기본 브랜치가 됩니다. master를 기본 브랜치로 사용하기 위해선 master를 먼저 push해야합니다.
    ```bash
    git checkout master
    git push
    ```
    develop도 동일한 방법으로 push합니다. 
    ```bash
    git checkout develop
    git push
    ```


-[실습을 진행할 코드를 업로드하였습니다. 이제 CodeCommit에 CodeGuru를 연결하도록하겠습니다.](/ko/setup/codeguru-reviewer) 