---
title: "소개"
weight: 10
pre: "<b>1. </b>"
tag:
  - Pipeline
  - CodeCommit
  - CodeBuild
  - CodeDeploy
  - CI/CD
  - UnitTest
---

{{% notice note %}}
만약 CI/CD와 CodeSeries에 대한 개념과 내용을 알고 있다면, [2단계(실습 환경 소개)](/setup)로 넘어가세요.
{{% /notice%}}

 ![problem0](/images/gitbranchenv2.svg)


|이름|설명|
|---|---|
| **master** | Production 코드 또는 Production-ready 코드 |
| **develop** | Integration 브랜치, 개발이 일어나는 브랜치 |


실습환경은 master와 develop 두개의 브랜치로 진행합니다. 
각각의 브랜치는 **Code Pipeline**을 이용하여 빌드와 배포 환경이 구성되어 있으며 develop 브랜치에 변경된 사항은 개발환경으로, master 브랜치에 변경된 사항은 프로덕션 환경으로 즉각적으로 배포됩니다.

 ![problem0](/images/gitbranch3.svg)

그렇기 때문에 병합시 변경된 코드리뷰와 유닛테스트 결과는 매우 중요하며 이것은 즉각적으로 개발자에게 전달될 수 있어야합니다. 

이 실습은 develop의 변경사항이 master로 병합될때 자동화된 **unit test**의 결과를 CodeBuild로 시각화 하는 내용과 **CodeGuru**를 사용하여 자동화된 코드 검토를 통해 안전하게 병합되는 방법을 소개하고 있습니다. 


- [이제 실습에 사용할 서비스들과 CI/CD의 개념에 대하여 설명하겠습니다.](/ko/introduction/cdci)
