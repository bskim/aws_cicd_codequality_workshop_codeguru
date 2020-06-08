---
title: "CodeGuru AWSSDK"
weight: 42
pre: "<b>4-2. </b>"
---

1. pull-request에 어떤 코드리뷰가 진행됬는지 확인해보겠습니다. (5분정도 걸릴 수 있습니다.)

1. CodeCommit의 콘솔로 가기: https://console.aws.amazon.com/codecommit
    
1. 왼쪽 Source의 Repositories를 선택하고 concurrencysample을 누릅니다. 
    ![pr1](/images/pc-codecommit-select.png)

1. 왼쪽 Source의 Repositories의 Pull requests를 `pr-concurrencytest`를 선택합니다. 
    ![pr2](/images/pr-solve-select.png)

1. CodeCommit과 Repository가 연결되어있다면 아래와 같은 화면이 나옵니다. 상단의 Activity를 선택합니다. 
    ![pr3](/images/pr-solve-comment.png)

1. 아무런 문제가 없는 줄 알았던 코드에 코드리뷰 코멘트가 달렸습니다. 
     ![pr4](/images/pr-awssdk2.png)

1. AWS SDK를 사용하기위해 코드에 넣었던 AccessKey와 SceretKey같은 장기 엑세스 키보다 임시보안증명(IAM을 사용하라는 가이드입니다. 이렇듯 CodeGuru가 AWS SDK를 올바르게 사용하는 방법과 문제점을 알려줍니다. 이런것들은 단순한 유닛테스트에서는 발견할 수 없는 내용이군요!

1. 또한 CodeGuru가 제안한 내용이 정말 유용한지 피드백을 통해 평가할 수 있습니다. 이것들이 더 나은 CodeGuru의 Comment를 생성하는데 기여할 수 있습니다.
    
-[또 어떤 문제가 있을까요?](/ko/codegurupr/solve-concurrency)
 
