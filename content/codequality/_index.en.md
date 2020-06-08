---
title: "Program Code"
weight: 30
pre: "<b>3. </b>"
---

{{% notice note %}}
Read this chapter to find out the cause of the detailed source code error.
[If you want to skip, directly go to solution..](/en/codequality/solve).
{{% /notice %}}


let`s look at the code first.
====================

{{% notice note %}}
ConcurrencySample Code is written in Java, Gradle.
{{% /notice %}}

{{% notice warning %}}
This code has a problem.
{{% /notice %}}

1. This is the structure of the source code. 
    
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

1.  let's take a look at the **SingletonRepo** file. **SingletonRepo** can only have one instance in the program. And sigletonsrepo have one HashMap. let's look at the putKey() function, which is the core of this class and lab.

    ```java
    public Object putKey(int product_code, int product_price, int tname) {           
        if (map.containsKey(product_code)) {
            return map.get(product_code);
        }else{
            return map.put(product_code, new Concurrency(product_code,"test"));
        }
    }
    ```
    putKey works is simple. Check that HashMap has a number with containKey() and if not, save the number with put().

    ![source01](/images/structure_same_single.svg)
1. If the HashMap already has the same value, don't put it.
    ![source01](/images/structure_same_fail4.svg)

1. **BasicSynchronization** calls pukey() of SingletonRepo and inserts a randomly generated number between 0 ~ 10000 in 3000 times.

1. **ConcurrencyCheckout** is Main class. This class creates 5 BasicSynchronizations and starts 5 threads.
    ![source](/images/structure.svg)
1. this program repeats input to one HashMap by 5 threads.

--------------------




So what is the problem with this program?
====================

1. This code has a concurrency issue. if it call two PutKey() from two threads at the same time. What will happen?
![problem0](/images/strustured-same-function.svg)
    
    The putkey () of both threads will enter the same number in the HashMap and increment the Call Count.

    ```java
    if (map.containsKey(product_code)) { 
        return map.get(product_code);
    }else{
        return map.put(product_code, new Concurrency(product_code,"test")); <-----first, second threadn function doing.
    }
    ```
1. The number is entered only once, but the call count is increased twice.
1. HashMap is not thread-safe. The code above is dangerous because get and put don't guarantee atomicity. 
1. If the number of threads is increased and the number of putkey calls executed simultaneously increases, the result cannot be guaranteed.
1. An error occurs because the same problem appears in the UnitTest being executed. **SingletonRepotests**, a unit test that is performed, creates 8 threads and raises the count one by one when an input occurs in the HashMap. And after all the work is done, the number of values entered in the HashMap is compared with the number of occurrences. If the values are the same, the number of inputs and the number of HashMaps are the same, so the function worked correctly.

1. However, UnitTest will continue to fail because the current code was programmed without considering concurrency. Of course, if you are very lucky, the test may succeed. However, to prevent this, **SingletonRepotests** performs the same test 1000 times.

-[So how do you solve this problem?](/en/codequality/solve)
