---
title: "CodeGuru Profiler"
weight: 50
pre: "<b>5. </b>"
---

We will create **CodeGuru Profiler groups**. This is where you can see the data of Profiling.

1. Go to the CodeGuru console: https://console.aws.amazon.com/codeguru


2. Select **Profiling groups** from the Profiler on the left menu. Then select `concurrencysample-profiler`.
    ![codeguru01](/images/codeguru-profiler-show.png)


3. You can see the analysis by CodeGuru Profiler. You can estimate the amount of time, percent, and cost per function. In addition, the results of profiling can be analyzed to provide reports that require improvement.
    ![codeguru01](/images/codeguru-profiler-analytics.png)

### Overview Visualization

1. An overview visualization can help you find specific call stacks that lead to inefficient code. You can find code that is running on the CPU by looking for flat tops in the visualization. It is an area where the CPU is doing work directly in that function and not a callee.


   ![codeguru01](/images/codeprofiler-cpu-zoom.png)


### Inspect Visualization

An inspect visualization is useful when you want to analyze a frame that appears in many places. It groups all of the frames with the same name together in the middle of the visualization. Children (callees) are merged and shown above the selected frame. Parents (callers) are merged and shown below the selected frame.


   ![codeguru01](/images/codeprofiler-inspect.png)

### Hotspot Visualization

A hotspots visualization can be used to investigate functions that are by themselves computationally expensive. It shows a top-down view of your profile. The functions consuming the most application time are at the top of the visualization. At the bottom of the visualization are the entry point functions.

   ![codeguru01](/images/codeprofiler-hotspots.png)

### Recommendations Report

Amazon CodeGuru Profiler makes recommendations you can use to optimize your applications. Each recommendation includes information about why the recommendation was made, a description, suggested resolution steps, and the stack locations that were the source of the recommendation.

   ![codeguru01](/images/profiler-report.png)

Reusing the AWS Client seems to be able to more optimize the program.
You can optimize the software using this variety of information.

-[Now that the training is finish!, Let`s delete the resources created.](/en/cleanup)    