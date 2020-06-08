---
title: "해결 방법"
weight: 53
pre: "<b>. </b>"
---

1. HashMap을 **ConcurrenctHashMap**으로 변경하면됩니다. **ConcurrenctHashMap**은 Thread-safe하게 설계되었기 때문에 Multi-threaded환경에서 안정적으로 동작하고 Hashtable, synchronized map보다 조금 더 나은 성능을 가지고 있습니다. **ConcurrenctHashMap**은 put을 할때 해당 맵에 lock을 걸기 때문에 동시에 같은 키가 put되는 것을 막을 수 있습니다.

1. Cloud9에서 **SingletonRepo.java**파일을 엽니다. 
![cloud901](/images/unittest-fix.png)

1. 아래 HashMap을 ConcurrentHashMap으로 변경합니다. 
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

1. 최종 **SingletonRepo.java**는 아래와 같습니다. 
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
1. 이제 변경사항을 다시 Push 해줍니다. 
    ```bash
    git add .
    git commit -m "fix singletonrepo.java"
    git push
    ```

1. 그리고 잠시 후 Report를 생성할때 확인 한 것처럼 Build의 Build project의 concurrencysample을 확인하면 빌드가 성공해 있는것을 볼 수 있습니다. 
    ![cloud901](/images/codequality-solve.png)

1. Report도 확인해 봅시다. 아까 Build의 **Report group**에서 Concurrency-Unittest-Report를 선택하면 100%로 통과된 결과를 확인 할 수 있습니다.  
    ![cloud901](/images/codequality-100.png)

1. 모든 테스트를 통과했기 때문에 Pipeline의 과정에 따라 자동으로 dev 환경에 배포까지 완료되었습니다. 

-[이제 프로덕션 환경에 배포하기 위해  master로 pull-request를 생성하겠습니다.](/ko/codegurupr)

