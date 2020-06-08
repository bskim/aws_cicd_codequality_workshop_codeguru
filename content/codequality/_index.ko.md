---
title: "프로그램 분석"
weight: 30
pre: "<b>3. </b>"
---

{{% notice note %}}
자세한 오류의 원인을 파악하고 싶으면 이 챕터를 읽어주세요.
[Skip 하고 싶으시면 여기서 바로 해결방법으로 넘어가시면 됩니다.](/ko/codequality/solve)
{{% /notice %}}


먼저 코드를 살펴봅시다.
====================

{{% notice note %}}
ConcurrencySample Code는 Java,Gradle로 작성되었습니다. 
{{% /notice %}}

{{% notice warning %}}
이 코드는 문제점을 가지고 있습니다.
{{% /notice %}}

1. 소스코드의 구조는 아래와 같습니다. 
    
    ```bash
    -src
        -main/java/com/example/
            -restservice
                -BasicSynchronization.java
                -ConcurrencyCheckout.java
                -SingletonRepo.java
            -s3
                -AwsCredentials-sample.propertie
                -AWSFileMapper.java
                -FileMapper.java
    ```

1.  **SingletonRepo**파일을 살펴보도록 하겠습니다. **SingletonRepo**는 프로그램에서 오직 단 하나의 instance만 가질 수 있습니다. 그리고 내부에 하나의 HashMap을 가지고 있습니다. 이 클래스와 실습의 핵심이 되는 putKey()함수를 살펴보도록 하겠습니다. 
    ```java
    public Object putKey(int product_code, int product_price, int tname) {           
        if (map.containsKey(product_code)) {
            return map.get(product_code);
        }else{
            return map.put(product_code, new Concurrency(product_code,"test"));
        }
    }
    ```
    putKey의 동작 방식은 간단합니다. containKey()로 HashMap에 숫자가 있는지 확인 하고 없을 경우 put()으로 숫자를 저장합니다. 

    ![source01](/images/structure_same_single.svg)
1. HashMap에 이미 동일한 값이 있다면 값을 입력하지 않습니다. 
    ![source01](/images/structure_same_fail4.svg)

1. **BasicSynchronization**는 SingletonRepo의 putKey함수를 호출하여 0~10000사이 임의로 생성한 숫자를 3000번 집어 넣습니다.

1. **ConcurrencyCheckout**은 Main을 포함하고 있는 Class입니다. 이 함수는 BasicSynchronization를 5개 생성하여 5개의 쓰레드를 시작시킵니다. 
    ![source](/images/structure.svg)
1. 즉 이 프로그램은 **ConcurrencyCheckout**에서 생성한 5개의 쓰레드가 하나의 HashMap에 입력을 반복합니다. 

--------------------




그럼 이 프로그램은 무슨 문제점을 가지고 있을까요?
====================
1. 이 코드는 동시성 문제를 가지고 있습니다. 만약 두개의 쓰레드에서 두개의 PutKey()를 거의 동시에 호출하면 어떻게 될까요?
    ![problem0](/images/structure_same_double.svg)
    
    만약 첫번째 함수의 putkey가 완료되지 않을때 두번째 함수의 putkey가 호출된다면, 두번째 함수도 HashMap에 동일한 숫자를 입력하고 Call Count를 증가시킬 것입니다. 
    ```java
    if (map.containsKey(product_code)) { 
        return map.get(product_code);
    }else{
        return map.put(product_code, new Concurrency(product_code,"test")); <-----첫번째 함수 진행중.두번째 함수 진행중.
    }
    ```
1. 숫자는 한번밖에 입력이 되지 않았는데 Call Count는 두번 증가하게 된 것입니다. 
1. HashMap은 전혀 Thread-safe하지 않습니다. get과 put이 원자성을 보장하지 않기 때문에 위와 같은 코드는 위험합니다. 
1. Thread가 많아지고 동시에 수행되는 putkey의 call이 늘어난다면 결과의 동일성을 보장할 수 없습니다. 


1. 수행중인 UnitTest에서도 이와같은 문제가 나타나기 때문에 error가 발생합니다. 수행되는 유닛테스트인 **SingletonRepotests**는 8개의 쓰레드를 생성시킨 뒤 HashMap에 입력이 일어날 경우 count를 하나씩 올립니다. 그리고 모든 작업이 끝난 후 HashMap에 입력된 값의 갯수와 입력이 일어난 횟수를 비교합니다. 값이 같다면 입력이 일어난 횟수와 HashMap이 가지고있는 갯수가 같으니 함수가 올바르게 동작한 것입니다. 

1. 하지만 현재 코드는 동시성을 고려하지 않고 프로그래밍했기 때문에 UnitTest가 계속 실패할 것입니다. 물론 아주 운이 좋다면 테스트가 성공할 수도 있습니다. 하지만 그럴 경우도 방지하기위해 **SingletonRepotests**는 동일한 테스트를 1000번 수행합니다. 

-[그럼 이 문제는 어떻게 해결해야 할까요?](/ko/codequality/solve)

