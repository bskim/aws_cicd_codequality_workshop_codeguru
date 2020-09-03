---
title: "CodeGuru Concurrency"
weight: 43
pre: "<b>4-3. </b>"
---

1. 스크롤을 내려거나 올려보면 또 다른 코멘트가 달려있는 것을 확인할 수 있습니다. 
     ![pr4](/images/pr-solve-comment-show.png)
     concurrentHashMap이 Thread-safe한 자료구조라고 생각했는데 한가지 문제점이 있었습니다. ConcurrentHashMap은 성능을 위해 put명령을 수행할 때 Map 전체에 Lock을 걸지 않습니다. 물론 함수에 synchronized를 선언하여 동기화 할 수는 있지만 이러면 결국 Single-Thread에서 도는것과 같기 때문에 성능에 문제가 생길 수도 있습니다. 

1. **CodeGuru**가 지적한 내용을 좀 더 자세히 살펴보면 다음과 같습니다. 
    ```java
    if (map.containsKey(product_code)) { <-----두번째 함수 진행중.
        return map.get(product_code);
    }else{
        return map.put(product_code, new Concurrency(product_code,"test")); <-----첫번째 함수 진행중.
    }
    ```

1. **CuncurrenctHashMap**의 put()가 map 전체에 lock을 걸지 않아 containsKey()의 결과를 보장할 수 없습니다. 동시성문제는 간단한 코드나 사옹량이 적은 규모라면 발생하기 매우 어려운 에러입니다. 하지만 만약 에러가 생겻을 경우 ConcurrentHashMap의 정확한 동작방벙을 이해하고 있지 않다면 문제를 수정하기 매우 어려울 것입니다. CodeGuru는 이러한 문제점들을 찾아낼 수 있습니다. 또한 적절한 해결책도 제공하고 있습니다. 

1. **CodeGuru Reviewer**가 제안한 대로 put(), containsKey() 함수 대신 putIfAbsent()함수를 한번만 수행하여 원자성을 보장할 수 있습니다. 
    해당코드를 아래와 같이 수정하겠습니다. 
    ```diff
    -if (map.containsKey(product_code)) { 
    -    return map.get(product_code);
    -}else{
    -    return map.put(product_code, new Concurrency(product_code,"test"));
    +return map.putIfAbsent(product_code,new Concurrency(product_code,"test", date));
    ```
1. SingletonRepo.java의 전체 코드는 아래와 같습니다. 
    ```java
    package com.example.concurrencyservice;

    import java.text.DateFormat;
    import java.text.SimpleDateFormat;
    import java.util.concurrent.*;

    public class SingletonRepo {

        private ConcurrentHashMap<Integer, Concurrency> map = new ConcurrentHashMap<>();
        DateFormat df = new SimpleDateFormat("yyyy-MM-dd");
        private static SingletonRepo singletonrepo = null;

        private SingletonRepo() {}

        public synchronized static SingletonRepo getInstance() {
            if (singletonrepo == null) {
                singletonrepo = new SingletonRepo();
                System.out.println("singleton repo instance created");
        //     count = 0;
            }
            return singletonrepo;
        }
    

        public Object putKey(int product_code, int product_price, int tname) {            
            return map.putIfAbsent(product_code, new Concurrency(product_code,"test", date));            
        }
        public int getMapCount() {
            return map.size();
        }
        public void clearHashMap() {
            map = new ConcurrentHashMap<>();
        }
        public Concurrency getKey(int product_number) {
            if (!map.containsKey(product_number)) {
                return null;
            } else {
                return map.get(product_number);
            }
        }
    }
    ```
    코드를 수정한 뒤 Push 합니다. 

    ```bash
    git add .
    git commit -m "fix put(), containerKey()-> putifAbsent()"
    git push
    ```

1. 문제가 수정되었으므로 Pull-Request를 종료하겠습니다. AWS 콘솔 오른쪽 상단의 Merg버튼을 누릅니다. 
    ![pr3](/images/pr-solve-fin2.png)

1. master는 변경사항이 없었으므로 Fast forward merge를 선택합니다. Source는 develop이기 때문에 `Delete source branch develop after merging?`의 체크박스는 해제합니다. 
    ![pr3](/images/pr-solve-merge.png)


1. 왼쪽 메뉴의 Pipeline의 pipelines 선택합니다. 이제 develop의 코드가 master로 들어가면서 빌드가 진행되는 것을 볼 수 있습니다. 
    ![pr3](/images/pr-solve-merge-deploy.png)
 

1. 잠시 후 master의 빌드와 배포가 완료 된 것을 볼 수 있습니다. 새로 개발,변경한 코드가 프로덕션 환경에 안전하게 반영되었습니다.  
    ![pr3](/images/pr-solve-merge-deploy2.png)

1. 이렇게 CD/CI 파이프라인을 사용하여 코드의 수정사항을 안전하게 master로 반영 할 수 있습니다. 또한 개발자는 **Commit**과 **push**만으로도 손쉽게 코드의 테스트 결과와 과정을 알 수 있습니다.  
    
1. UnitTest와 CodeReview는 코드풀질을 높혀줄 수 있는 매우 좋은 방법중에 하나입니다. 각각의 과정에 **CodeBuild Report**와 **CodeGuru Reviwer**기능을 사용하여 더 안전하고 효과적인 코드빌드와 UnitTest를 하실 수 있습니다. 

[이제 실제 배포되서 돌아가는 프로파일링 결과를 확인하도록 하겠습니다.](/ko/codeguruprofiler)    
