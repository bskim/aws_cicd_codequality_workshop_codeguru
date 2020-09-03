---
title: "CodeGuru Reviewer"
weight: 40
pre: "<b>4. </b>"
---

{{% notice note %}}
문제점을 해결한 Code를 Pull-Request를 통해 master로 병합하여 최종코드를 프로덕션환경으로 배포합니다.
{{% /notice %}}

1. 이제 프로덕션에 사용할 코드가 완성되었습니다. develop 브랜치의 코드는 모든 유닛테스트를 문제없이 통과하였기 때문에 프로덕션 환경에 배포할 것입니다. 일반 개발자는 보통 master 브랜치에 직접 push할 수 있는 권한이 없습니다. 그래서 pull-request를 통해 시니어개발자 또는 동료개발자와의 코드리뷰를 거친 후 master에 반영할 예정입니다. 혹시 모를 다른 문제점이 있을 수도 있으니까요. 


1.	pull-request를 생성하기위해 CodeCommit 콘솔로 갑니다. : https://console.aws.amazon.com/codesuite/codecommit/repositories     

1. 왼쪽 Source의 Repositories를 선택하고 concurrencysample을 누릅니다. 
    ![pr1](/images/pc-codecommit-select.png)

1. 왼쪽 Source의 Repositories의 Pull requests를 선택하고 오른쪽 위 **Create pull request**를 누릅니다. 
    ![pr2](/images/pc-codecommit-prselect.png)

1. Create pull request의 Destination은 **master** Source는 **develop**으로 설정한 후 **Compare**버튼을 누릅니다. 
    ![pr3](/images/pc-codecommit-createpr.png)

1. Details의 Title에 `pr concurrencytest`를 입력하고 Description에 `for workshop`을 입력하고 오른쪽의 **Create pull request**를 선택합니다. 
    ![pr3](/images/pc-codecommit-fin.png)

-[pull-request를 생성하였습니다. 이제 어떤 일이 일어나는지 확인하겠습니다. ](/ko/codegurupr/solve-awssdk)
