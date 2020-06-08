---

title: "CodeBuild Report"
weight: 26
pre: "<b>2-5. </b>"

---

### Let`s Add to CodeBuild Report Group

this lab use unit tests are using Junit. The result of the unit test is published in xml, and the developer should be able to use this to know which unit test his code did not pass.

Go to the Codebuild console : https://console.aws.amazon.com/codebuild

1. Select **Report groups** in the right Build tab. Select **Create report group** at the top right.
    ![codebuild02](/images/codebuild-report.png)

1. Enter `Concurrency-Unittest-Report` in **Report group name** of Rport group configuration. Uncheck the box for **Export to Amazon S3**.
    ![codebuild02](/images/cloudbuild-report-2.png)

1. To copy the ARN of the report groups, **Concurrency-Unittest-Report** from **Report groups**.
    ![codebuild02](/images/codebuild-report-arn.png)

1. The results of the Unittest here will now be shown. Copy the contents of **Report group ARN** of Configuration.
    ![codebuild02](/images/codebuild-report-copy-arn.png)

1. Now let`s go back to **Cloud9** and edit **buildspec.yml**. **buildspec.yml** is located in ConcurrencySample's root directory. 
    ![DataLakeStorage03](/images/cloudbuild-report-cloud9.png)
    Double-click the file to add content. Paste the **Report group ARN** to `<YOUR-REPORT-GROUP-ARN>`.
    ```yml
    reports:
      <YOUR-REPORT-GROUP-ARN>:
      files:
        - '**/*'
      base-directory: 'build/test-results/test'
    ```

1. this is final code of **buildspec.yml**.
    ```yml
    version: 0.2
    
    phases:
      install:
        runtime-versions:
          java: corretto11
        commands:
          - java -version
          - gradle -version
      build:
        commands:
          - ./gradlew clean build
    reports:
      <YOUR-REPORT-GROUP-ARN>:
        files:
          - '**/*'
        base-directory: 'build/test-results/test'      
    artifacts:
      files:
        - '**/*'
      name: concurrencysample-$(date +%Y-%m-%d) 
    
    ```
1. Commit and push them to codecommit.
    ```bash
    cd ConcurrencySample
    git add .
    git commit -m "change Buildspec.yml"
    git push
    ```

1. let`s check if the changes have been reflected. Select **concurrencysample** by selecting **Build projects** in **Build** on the left menu.
    ![codebuild02](/images/codebuild-report-confirm.png)

1. You can see the failed build. let`s click on the content to confirm.
    ![codebuild02](/images/codebuild-report-buildfail.png)
    If you look at the message below, you can see that the build was successful. But you can see UnitTest failed.
    ![codebuild02](/images/codebuild-report-unittestfail.png)
    In this way, it is difficult to see the details of how and what tests have passed. so you can see to the report file generated in the build folder or view the xml file. But you can easily check the results of each build by using the previously linked **CodeBuild Report**.
    let`s go **Report groups** and check the uploaded report.
1. Select **Report groups** from the left Build menu. Then select the **Cuncurrency-Unittest-Report** you created earlier.
    ![codebuild02](/images/codebuild-report-show.png)

1. You can see the success and execution time in a graph and click the report in the report history at the bottom to see the details of UnitTest. It is much more easy to check than the console.
    ![codebuild02](/images/codebuild-report-graph.png)
    ![codebuild02](/images/codebuild-report-detail.png)
    ![codebuild02](/images/codebuild-report-detail2.png)

    

-[Let`s see why the unit test failed and how to fix it.](/en/codequality) 
