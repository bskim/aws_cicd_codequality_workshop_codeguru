---
title: "실습 환경 셋업"
weight: 20
pre: "<b>2. </b>"
---

{{% notice note %}}
다음 장에서 생성한 CloudFormation의 스택은 이 실습환경과 master와 develop의 CI/CD 파이프라인을 전부 포함하고 있습니다. 
{{% /notice%}}

본 실습은 코드품질을 높히기 위한 과정을 AWS의 서비스를 사용하여 어떻게 진행하는지를 보여드립니다. 각각의 과정을 모두 자동화하여 개발자가 최소한의 노력으로 코드를 Commit하고 테스트하고 배포할 수 있습니다. 배포와 테스트가 이루어지는 환경은 다음과 같습니다. 

#### 실습환경
![AWS-Code-Cycle](/images/aws.svg)

#### 사용 서비스
![AWS-Code-Cycle](/images/awsservice.svg)


| 이름 | 설명|
|:---|:---|
| **CodeCommit** | 코드저장소는 **CodeCommit**이며 개발 코드는 **JAVA**이며 Gradle을 사용합니다. Master Branch에서 Prod환경으로 바로 배포합니다. 개발자의 소스코드 변경과 테스트는 Develop Branch에서 이루어집니다. |
| **CodeBuild** | 빌드툴은 **CodeBuild** 입니다. UnitTest를 위해 Junit을 사용할 것이며 결과는  xml로 출력합니다. 출력된 Report는 CodeCommit의 보고서 기능을 사용하여 콘솔에서 바로 확인합니다. |
| **CodeDeploy** | 테스트가 통과된 코드는 자동으로 Dev환경에 배포됩니다. Develop Branch에 Push된 코드는 DevWebApp01인스턴스에 배포되며 CodeGuru의 프로파일러 기능을 사용하여 성능분석을 시작합니다. 그리고 모든 테스트가 통과되어 Master에 Merge되면 코드는 ProdWebApp01로 자동 배포됩니다. | 
| **CodePipeline** | 위 일련의 과정을 **CodePipeline**으로 시각화합니다. 개발자는 Push된 코드가 어느부분에 문제가 있는지 바로 알아 차릴 수 있습니다. |
| **CodeGuru** | Pull-Request시 자동으로 Code-Review를 진행합니다. DevWebapp01에 배포된 코드의 프로파일링을 수행합니다. |


-[CloudFomration을 이용하여 실습환경을 셋팅해보겠습니다.](/ko/setup/lab-setup) 
