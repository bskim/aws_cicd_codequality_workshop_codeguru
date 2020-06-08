---
title: "CodeGuru Profiler"
weight: 50
pre: "<b>5. </b>"
---

**CodeGuru Profiler groups**를 만들겠습니다. 이곳에서 실제 돌아가는 프로그램의 Profiling의 결과를 볼 수 있는 곳입니다. 

CodeGuru 콘솔로 가기: https://console.aws.amazon.com/CodeGuru

왼쪽 메뉴의 Profiler의 **Profiling groups**를 선택합니다. 그리고 `concurrencysample-profiler`를 선택합니다. 
    ![codeguru01](/images/codeguru-profiler-show.png)


CodeGuru Profiler가 분석한 내용을 볼 수 있습니다. 함수당 수행한 시간과 퍼센트, 대략적인 비용을 예상할 수 있습니다. 또 한 프로파일링의 결과를 분석하여 개선해야할 점들을 리포트로 제공할 수도 있습니다. 
    ![codeguru01](/images/codepofiler-cpu-putkey.png)

함수에 마우스를 올리면 자세한 정보 (예 : 전체 이름 및 스레드 상태)를 얻을 수 있습니다. 또한 프레임의 서브 스택에 존재하는 메소드의 활성 CPU 비용을 볼 수도 있습니다. 확대 할 프레임을 클릭하면 하단의 ALL 블록을 사용하여 프로파일의 전체보기로 돌아갑니다.


### Overview Visualization

Overview visualization은 비효율적 인 코드로 이어지는 특정 호출 스택을 찾는 데 도움이됩니다. visualization에서 평평한 상단을 찾아 CPU에서 실행중인 코드를 찾을 수 있습니다. 이 영역은 CPU가 직접 수행한 함수를 보여줍니다. 


   ![codeguru01](/images/codeprofiler-cpu-zoom.png)


### Inspect Visualization

Inspect Visualization는 여러 곳에 나타나는 프레임을 분석 할 때 유용합니다. 시각화 도중 동일한 이름을 가진 모든 프레임을 함께 그룹화합니다. 선택한 프레임 위에 자식(callees)은 병합되어 표시됩니다. 부모(callers)는 병합되어 선택한 프레임 아래에 표시됩니다.

   ![codeguru01](/images/codeprofiler-inspect.png)

### Hotspot Visualization

Hotspot Visualization를 사용하여 비싼 기능을 조사 할 수 있습니다. 하향식보기가 표시됩니다. 가장 많은 시간을 소비하는 기능은 시각화의 최상위에 있습니다. 

   ![codeguru01](/images/codeprofiler-hotspots.png)

### Recommendations Report

일반적으로 하루이상의 profiling 을 수행하게 되면 Amazon CodeGuru Profiler는 애플리케이션을 최적화하는 데 사용할 수있는 권장 사항을 제시합니다. 각 권장 사항에는 권장 사항에 대한 정보, 설명, 제안 된 해결 단계 및 권장 사항의 스택 위치가 포함됩니다.

   ![codeguru01](/images/profiler-report.png)

보고서의 내용이라면 AWS SDK를 좀더 효율적으로 사용하여 프로그램을 최적화 할 수 있을 것 같습니다. 
이런 다양한 정보들을 사용하여 소프트웨어를 최적화 할 수 있습니다. 

-[이제 실습이 끝났으니 지금까지 생성한 리소스를 지우도록하겠습니다.](/ko/cleanup)    