---
title: "CodeGuru Profiler"
weight: 25
pre: "<b>2-4. </b>"

---

### **CodeGuru Profiler**를 WebApp 서버와 연동하겠습니다.  

CodeGuru 콘솔로 가기: https://console.aws.amazon.com/codeguru

1. 왼쪽 메뉴의 Profiler의 **Profiling groups**를 선택합니다. 
    ![codeguru01](/images/codeguru-profiler-select.png)

1. 오른쪽 상단의 **Create profiling groups**를 선택합니다. 
    ![codeguru01](/images/codeguru-profiler-group.png)


1. **Create profiling group**의 **Profiling group details**의 **Name**에 `concurrencysample-profiler`를 입력합니다. 그리고 오른쪽 하단의 Create를 누릅니다. 
    ![codeguru01](/images/codeguru-profiler-create.png)


1. **Manage permissions for concurrencysample-profiler**박스의 **choose users and roles**에 `CodeQuality-Workshop-WebAppRole`을 입력합니다. 그럼 이전 CloudFormation에서 만들었던 Stack 인스턴스의 role이 나옵니다. 왼쪽 체크박스를 선택한 후 Save를 눌러 저장합니다.  
    ![codeguru01](/images/codeguru-profiler-webapp.png)

1. Profiler는 소스코드의 메인 클래스인 **ConcurrencyCheckout.java**의 main 에서 찾을 수 있습니다. 
    ```java
    public static void main(final String[] args) {
        // Start the profiler
        Profiler systemProfiler = Profiler.builder()
        .profilingGroupName("concurrencysample-profiler").build();
        systemProfiler.start();
        ...
    }
    ```
    만약 다른 보고서 그룹에 연동하시려면 profilingGroupName의 매개변수인 `concurrencysample-profiler`를 다른 **보고서 그룹**이름으로 지정해주세요. 

1. 이제 CodeGuru Profiler와 인스턴스간 연결이 끝났습니다.  

-[ Unit Test의 결과를 쉽게 볼 수 있도록 CodeBuild의 Report group을 만들도록 하겠습니다.](/ko/setup/codebuild) 
