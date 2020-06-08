---
title: "CI/CD with Code Series"
weight: 11
pre: "<b>1-1 </b>"
tag:
  - Code Series
---

## CI/CD란?(Continuous Integration/Continuous Delivery)


CI/CD는 빌드 및 테스트를 자동화하여 보다 짧은 주기로 고객에게 어플리케이션을 제공하는 방법입니다. 또한 개발자가 변경하는 새로운 코드들의 Merge로 인해 생기는 여러가지 문제를 해결하기위한 솔루션이기도 합니다. 특히 CI/CD는 소프트웨어 릴리스 프로세스 중 빌드 또는 통합 단계를 주로 가리키며, 어플리케이션의 라이프사이클 전체의 자동화와 모니터링을 제공합니다. 

![AWS의Pipeline](/images/continuous_integration.4f4cddb8556e2b1a0ca0872ace4d5fe2f68bbc58.png)

**CI**는 (Continuous Deployment)는 개발자들의 변경사항이 버그테스트를 거쳐 **Repository**에 자동으로 업로드되는 것을 뜻합니다. 
**CD**는 Continuous Deployment)는 개발자들의 변경사항이 모든 테스트를 거쳐 고객이 사용가능한 프로덕션 환경까지 자동으로 릴리즈 되는 것을 뜻합니다. 
결과적으로 CI/CD는 파이프라인으로 표현되는 실제 프로세스를 의미하고 어플리케이션 개발의 자동화화 모니터링을 추가하는것을 의미합니다. 

이것은 개발자가 최소한의 작업으로 본인의 코드를 테스트, 또는 실제 릴리즈까지 가능하게합니다. 그렇기 때문에 잘 구성된 CI/CD 파이프라인은 파이프라인에 셋팅된 자동 테스트들로 인해 코드 품질을 향상시킴과 동시에 개발 사이클을 앞당겨 전체적인 개발속도를 향상시킬 수 있습니다.

## 어떻게? 무엇을 사용해야 할까?

AWS에서 제공하는 **Code Series**를 사용할 수 있습니다. 코드시리즈는 완전관리형 서비스기 때문에 별도의 서버나 인프라가 필요 없습니다. 

![codeseries](/images/codeseries.svg)

1. **CodeCommit** : AWS CodeCommit은 안전한 Git 기반 리포지토리를 호스팅하는 완전관리형 소스 제어 서비스(Sorcecode Version Control)입니다
1. **CodeBuild** : AWS CodeBuild는 소스 코드를 컴파일하는 단계부터 테스트 실행 후 소프트웨어 패키지를 개발하여 배포하는 단계까지 마칠 수 있는 완전관리형의 지속적 통합 서비스입니다
1. **CodeDeploy** : AWS CodeDeploy는 Amazon EC2, AWS Fargate, AWS Lambda 및 온프레미스 서버와 같은 다양한 컴퓨팅 서비스에 대한 소프트웨어 배포를 자동화하는 완전관리형 배포 서비스입니다.
1. **CodePipeline** : AWS CodePipeline은 빠르고 안정적인 애플리케이션 및 인프라 업데이트를 위해 릴리스 파이프라인을 자동화하는 데 도움이 되는 완전관리형 지속적 전달 서비스입니다. 
 
- [ 그럼 UnitTest는 무엇인가요?](/ko/introduction/unittest)



