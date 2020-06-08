---
title: "CodeGuru Profiler"
weight: 24
pre: "<b>2-4. </b>"

---

### **CodeGuru Profiler** setup.

go to the CodeGuru console: https://console.aws.amazon.com/codeguru

1. Select **Profiling groups** from Profiler on the left menu.
    ![codeguru01](/images/codeguru-profiler-select.png)

1. Select **Create profiling groups** at the top right.
    ![codeguru01](/images/codeguru-profiler-group.png)


1. Enter `concurrencysample-profiler` in **Name** of **Profiling group details** in **Create profiling group**. click Create at the bottom right.
    ![codeguru01](/images/codeguru-profiler-create.png)


1. Enter `CodeQuality-Workshop-WebAppRole` in **choose users and roles** in the **Manage permissions for concurrencysample-profiler** box. Select the checkbox on the left and click Save to save. 
    ![codeguru01](/images/codeguru-profiler-webapp.png)

1. Profiler can be found in the main of the source code, **ConcurrencyCheckout.java**.
    ```java
    public static void main(final String[] args) {
        // Start the profiler
        Profiler systemProfiler = Profiler.builder()
        .profilingGroupName("concurrencysample-profiler").build();
        systemProfiler.start();
        ...
    }
    ```
    If you want to link to a different report group, please specify `concurrencysample-profiler`, the parameter of profilingGroupName, with a different **report group** name.

1. The connection between the CodeGuru Profiler and the instance is now complete. 

 -	[ create a report group of CodeBuild finished. let`s setup for easily see the results of Unit Test. ](/en/setup/codebuild) 


