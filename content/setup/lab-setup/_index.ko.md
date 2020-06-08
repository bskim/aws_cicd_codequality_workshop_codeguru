---
title: "CloudFormation"
weight: 21
pre: "<b>2-0. </b>"
---

## AWS 계정
{{% notice warning %}}
이미 AWS 계정을 가지고 있다면 즉시 이 실습의 가이드를 따라 진행할 수 있으나, **계정이 없다면** 먼저 AWS 계정을 만들어야 합니다.
{{% /notice %}}
AWS 계정 생성 및 활성화 가이드는 다음 [링크](https://aws.amazon.com/ko/premiumsupport/knowledge-center/create-and-activate-aws-account/)를 참조하시기 바랍니다.  

{{% notice info %}}
실습은 **us-west-2 (오레곤) 리전을 선택**합니다. 해당 실습은 **다른 AWS 리전에서는 작동하지 않습니다.**  
본 실습 시작 전, 실습에 필요한 리소스는 AWS CloudFormation을 사용하여 구성한 다음, CodeGuru와 Codebuild Report를 별도로 구성합니다.
{{% /notice %}}

## IAM 사용자
AWS 계정을 생성했지만 직접 IAM 사용자를 생성하지 않은 경우, IAM 콘솔을 사용하여 IAM 사용자를 생성 할 수 있습니다. 다음 스텝에 따라 Administrator (관리자) 사용자를 생성합니다. 이미 관리자 사용자가 있다면, 다음 IAM 사용자 생성 작업을 건너 뜁니다. 

1.	AWS 계정 이메일 주소와 비밀번호를 사용하여 AWS 계정의 **Root** 사용자로 [IAM 콘솔](https://console.aws.amazon.com/iam/) 에 로그인 합니다.
1.	IAM 콘솔 왼쪽 메뉴 패널에서 **Users** (사용자)를 선택한 다음 **Add user** (사용자 추가)를 클릭합니다.
1.	**User name** (사용자 이름)은 `Administrator`로 입력합니다.
1.	**AWS Management Console access** 체크박스를 선택하고, **Custom password**를 선택한 다음 비빌번호를 입력합니다. 
1.	**Next: Permissions** (다음: 권한)을 클릭합니다.
![IAMPermission](/images/iam_user_01.png)
1.	**Attach existing policies directly** (기존 정책 직접 연결)를 선택하고 **AdministratorAccess** 정책에 체크박스를 선택하고 **Next: Tags** (다음: 태그)를 클릭합니다.
![IAMPolicy](/images/iam_user_02.png)
1.	**Next: Review** (다음: 검토)를 클릭합니다.
1.	Administrator 사용자에 AdministratorAccess 관리형 정책이 추가 된 것을 확인하고 **Create user** (사용자 만들기)를 클릭합니다.
1.	이제 **Root** 사용자를 **로그아웃**하고 새로 생성한 **Administrator** 사용자로 **로그인**을 합니다. 다음 URL을 사용하여 로그인 할 수 있습니다.
> `https://<your_aws_account_id>.signin.aws.amazon.com/console/`  
{{% notice warning %}}
<your_aws_account_id>는 본인 AWS 계정의 고유 ID를 입력합니다. Root 사용자로는 해당 실습을 진행할 때 에러가 발생할 수 있습니다. 반드시 admin 유저 계정으로 로그인하여 진행하세요.
{{% /notice %}}

## EC2 Key Pair
CloudFormaton template을 사용하여 실습에 필요한 기본 환경을 구성하려면 Amazon EC2 키 페어를 제공해야 합니다. 이미 EC2 키 페어가 있는 경우 다음 작업을 건너 뜁니다.
1.	**Administrator** 사용자로 AWS 콘솔에 로그인 한 다음 [EC2 콘솔](https://console.aws.amazon.com/ec2/)로 이동합니다.
1.	탐색 창의 **Network & Security** (네트워크 & 보안)에서 **Key Pairs** (키 페어)를 선택합니다.
1.	**Create Key Pair** (키 페어 생성)를 클릭합니다.
1.	**Key pair name** (키 페어 이름)에 새 key pair의 이름을 입력 한 다음 **Create** (생성)을 클릭합니다.
1.	.PEM 파일 형식의 Private Key (개인 키) 파일은 브라우저에서 자동으로 다운로드 됩니다. 개인 키는 다음 CloudFormation을 사용할 때 필요합니다.

## CloudFormation Template
AWS CloudFormation에서는 클라우드 환경에서 AWS 및 타사 애플리케이션 리소스를 모델링하고 프로비저닝할 수 있도록 공용 언어를 제공합니다. AWS CloudFormation을 사용하면 프로그래밍 언어 또는 간단한 텍스트 파일을 사용하여 자동화되고 안전한 방식으로 모든 지역과 계정에 걸쳐 애플리케이션에 필요한 모든 리소스를 모델링 및 프로비저닝할 수 있습니다.

AWS CodeQuality 실습에 필요한 AWS 리소스를 사전에 생성하기 위해 제공된CloudFormation template을 사용하여 CloudFormation stack을 생성합니다. 
개발환경과 프로덕션 환경을 위한 EC2와 VPC, 그리고 각각의 환경에 생서할 CodePipeline, CodeBuild, CodeDeploy, CodeCommit을 생성합니다.

CloudFormation 스택을 시작하려면, [Launch Stack 버튼](https://console.aws.amazon.com/cloudformation/home?region=us-west-2#/stacks/new?stackName=CodeQuality-Workshop&templateURL=https://sykang-productionapp.s3-us-west-2.amazonaws.com/vpc.template)를 클릭해서 CloudFormation 콘솔로 이동합니다.

{{% notice warning %}}
중요: 이 탬플릿은 us-west-2 (오레곤)을 위해 만들어졌으며 다른 AWS 리전에서는 작동하지 않습니다.
{{% /notice %}}

{{% button href="https://console.aws.amazon.com/cloudformation/home?region=us-west-2#/stacks/new?stackName=CodeQuality-Workshop&templateURL=https://sykang-productionapp.s3-us-west-2.amazonaws.com/vpc.template" icon="fab fa-aws" icon-position="left" %}}&nbsp;Launch Stack{{% /button %}}

스택 생성 단계에서 스택 이름을 입력하고 앞서 생성한 EC2 키 페어를 선택합니다. 그리고 나머지는 기본 값을 유지하고 마지막 단계에서 CloudFormation이 IAM 리소스를 생성할 때 커스텀 이름을 사용할 수 있게 **Acknowledge 체크박스를 선택**하고 **Create stack** (스택 생성)을 클릭합니다.


![CloudFormation_01](/images/cloudformation-specify-stack-details.png)
CloudFormation 스택을 완료하는 데 약 5분 정도 소요됩니다. CloudFormation 콘솔을 확인하고 아래와 같이 **CREATE_COMPLETE** 상태를 기다립니다.
![CloudFormation_03](/images/cloudformation-stacks-info.png)
{{% notice note %}}
스택 생성이 완료되면 AWS 계정에 실습을 실행하는 데 필요한 모든 기본 리소스가 준비 되어있습니다. **Outputs 탭**에서 **DevWebApp01의 이름**, **ProudWebApp01**의 이름이 표시됩니다.
{{% /notice %}}

-[이제 생성된 빌드 환경에 CI/CD파이프라인을 구축해 보겠습니다.](/ko/setup/cloud9) 




