---
title: "CodeGuru Concurrency"
weight: 43
pre: "<b>4-3. </b>"
---

1. Scroll down or look up to see another comment.
     ![pr4](/images/pr-solve-comment-show.png)
     I thought concurrentHashMap was a thread-safe data structure, but there was one problem. ConcurrentHashMap does not lock the entire map when performing put command for performance. Of course, you can declare a function to be synchronized and synchronize, but in this case, it is the same as turning in a single-thread, which can cause performance problems.

1. A more detailed what **CodeGuru** points out is as follows.
    ```java
    if (map.containsKey(product_code)) { <-----second function doing...
        return map.get(product_code);
    }else{
        return map.put(product_code, new Concurrency(product_code,"test")); <-----first function doing...
    }
    ```

1. The result of containsKey() cannot be guaranteed because put() of **CuncurrenctHashMap** does not lock the entire map. The concurrency problem is a very difficult error to occur if it is a simple code or a small thraed. However, if an error occurs, it will be very difficult to fix the problem if you do not understand the correct behavior of ConcurrentHashMap. CodeGuru can find these problems. It also provides a solution.

1. As suggested by **CodeGuru Reviewer**, you can guarantee atomicity by performing the putIfAbsent() function once instead of the put() and containsKey().
    We will fix the code as follows.
    ```diff
    -if (map.containsKey(product_code)) { 
    -    return map.get(product_code);
    -}else{
    -    return map.put(product_code, new Concurrency(product_code,"test"));
    +return map.putIfAbsent(product_code,new Concurrency(product_code,"test", date));
    ```
1. The full code of singletonRepo.java is here.. 
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
            return map.putIfAbsent(product_code,new Concurrency(product_code,"test", date));
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
    Edit the code and push. 

    ```bash
    git add .
    git commit -m "fix put(), containerKey()-> putifAbsent()"
    git push
    ```

1. the problem has been fixed, we will end the Pull-Request. Click the Merg button in the top right corner of the AWS console. 
    ![pr3](/images/pr-solve-fin2.png)

1. Since master has not changed, we choose Fast forward merge. Source is develop branch, uncheck the box of `Delete source branch develop after merging?`.
    ![pr3](/images/pr-solve-merge.png)


1. Select Pipeline pipelines from the left menu. Now you can see the build progress as the develop code goes into the master.
    ![pr3](/images/pr-solve-merge-deploy.png)
 

1. After a while, you can see that the master's build and deployment is complete. The newly changed code is safely merge in the production environment. 
    ![pr3](/images/pr-solve-merge-deploy2.png)

1. Using the CD/CI pipeline, modifications of the code can be safely reflected as the master. Also, developers can easily see the test results and process of the code by simply using **Commit** and **push**.
    
1. UnitTest and CodeReview are one of the best ways to improve code quality. For each process, you can use the **CodeBuild Report** and **CodeGuru Reviwer** to make code review and UnitTest safer and more effective.

-[Now let`s check the profiling results that are actually deployed and running.](/en/codeguruprofiler)    
 
