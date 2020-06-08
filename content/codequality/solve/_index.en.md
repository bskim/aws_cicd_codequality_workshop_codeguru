---
title: "Solution"
weight: 53
pre: "<b>5-3. </b>"
---

1. You can change HashMap to **ConcurrenctHashMap**. **ConcurrenctHashMap** is designed to be thread-safe, so it operates stably in a multi-threaded environment and has slightly better performance than Hashtable and synchronized map. **ConcurrenctHashMap** locks the map when you put it, so you can prevent the same key put at the same time.

1. Open the **SingletonRepo.java** file in Cloud9.
    ![cloud901](/images/unittest-fix.png)

1. Change the HashMap below to ConcurrentHashMap.
    ```diff
    +   import java.util.concurrent.*;
        ...
    -   private HashMap<Integer, Concurrency> map = new HashMap<>();
    +   private ConcurrentHashMap<Integer, Concurrency> map = new ConcurrentHashMap<>();

        ...
        
        public void clearHashMap() {
    +       map = new ConcurrentHashMap<>();
    -       map = new HashMap<>();
        }

    ```

1. The final **SingletonRepo.java** source code
    ```java
    package com.concurrencysample;

    import java.text.DateFormat;
    import java.text.SimpleDateFormat;
    import java.util.Date;
    import java.util.HashMap;
    import java.util.concurrent.*;

    import com.amazonaws.auth.AWSCredentials;
    import com.amazonaws.auth.AWSStaticCredentialsProvider;
    import com.amazonaws.auth.BasicAWSCredentials;
    import com.amazonaws.services.dynamodbv2.AmazonDynamoDB;
    import com.amazonaws.services.dynamodbv2.AmazonDynamoDBClientBuilder;
    import com.amazonaws.services.dynamodbv2.document.DynamoDB;
    import com.amazonaws.services.dynamodbv2.document.Item;
    import com.amazonaws.services.dynamodbv2.document.Table;
    import com.amazonaws.services.dynamodbv2.model.AttributeDefinition;
    import com.amazonaws.services.dynamodbv2.model.CreateTableRequest;
    import com.amazonaws.services.dynamodbv2.model.KeySchemaElement;
    import com.amazonaws.services.dynamodbv2.model.KeyType;
    import com.amazonaws.services.dynamodbv2.model.ProvisionedThroughput;
    import com.amazonaws.services.dynamodbv2.model.ScalarAttributeType;

    public class SingletonRepo {
        private static String ACCESS_KEY = "";
        private static String SECERET_KEY = "";
        private ConcurrentHashMap<Integer, Concurrency> map = new ConcurrentHashMap<>();
        DateFormat df = new SimpleDateFormat("yyyy-MM-dd");
        private static SingletonRepo singletonrepo = null;
        static AWSCredentials ac;
        static AmazonDynamoDB dynamodb;

        private SingletonRepo() {
        }

        public synchronized static SingletonRepo getInstance() {
            if (singletonrepo == null) {
                singletonrepo = new SingletonRepo();

                ac = new BasicAWSCredentials(ACCESS_KEY, SECERET_KEY);

                dynamodb = AmazonDynamoDBClientBuilder
                        .standard()
                .withRegion("us-west-2")
                .withCredentials(new AWSStaticCredentialsProvider(ac) )
                .build();
                System.out.println("singleton repo instance created");
            }
            return singletonrepo;
        }
        public Concurrency get(int product_code){
            return map.get(product_code);
        }

        public Concurrency putKey(int product_code ) {           
            Date date = Util.getRandomDate();
            if (map.containsKey(product_code)) {
                return map.get(product_code);
            }else{
                return map.put(product_code, new Concurrency(product_code,"test" , date));
            }   
        }
        public void delKey(int product_code ) { 
            if (map.containsKey(product_code)) {
                map.remove(product_code);
            }
        }
        public int getMapCount() {
            return map.size();
        }
        public synchronized void clearHashMap() {
            map.clear();
            map = new ConcurrentHashMap<>();
        }
        public Concurrency getKey(int product_number) {
            return map.get(product_number);  
        }
    }
    ```
1. push the changes again.
    ```bash
    git add .
    git commit -m "fix singletonrepo.java"
    git push
    ```

1. And if you check the `concurrencysample` of Build, you can see that the build was successful
    ![cloud901](/images/codequality-solve.png)

1. let`s also check the Report. If you select Concurrency-Unittest-Report in **Report group** of Build, you can see the result passed by 100%.
    ![cloud901](/images/codequality-100.png)

1. it passed all tests, it was automatically deploy to the dev environment according to Pipeline's process.

-[Now let`s create a pull-request for deployment code to production environment](/en/codegurupr)

