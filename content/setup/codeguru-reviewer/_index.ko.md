---
title: "CodeGuru Reviewer"
weight: 24
pre: "<b>2-3. </b>"

---

### **CodeGuru Reviewer**를 CodeCommit과 연동하겠습니다.  

CodeGuru 콘솔로 가기: https://console.aws.amazon.com/codeguru

1. 왼쪽 메뉴의 Reviewer의 **Associated repositories**를 선택합니다. 
    ![codeguru01](/images/codeguru-reviewer-select.png)

1. 오른쪽 상단의 **Associate repository**를 선택합니다. 
    ![codeguru01](/images/codeguru-associate-repository.png)

1. Repository details의 Source provider를 **AWS CodeCommit**으로 선택한 뒤 Repository location에서 **concurrencysample**을 선택합니다. 그리고 Associate를 누릅니다. 
    ![codeguru01](/images/codeguru-associate.png)

1. Codeguru의 Dashboard에서 연결된 concurrencysample을 확인하실 수 있습니다. . 
    ![codeguru01](/images/codeguru-fin.png)

1. 이제 CodeGuru와 CodeCommit의 연동이 끝났습니다. 

-[이제 CodeCommit에 CodeGuru의 Profiler를 연결하도록하겠습니다.](/ko/setup/codeguru-profiler) 
