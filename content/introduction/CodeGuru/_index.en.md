---
title: "CodeGuru"
weight: 13
pre: "<b>1-3 </b>"
tag:
  - CodeGuru
  - CodeReview
---

## AWS CodeGuru

Amazon CodeGuru is a machine learning service for automated code reviews and application performance recommendations. It helps you find the most expensive lines of code that hurt application performance and keep you up all night troubleshooting, then gives you specific recommendations to fix or improve your code. codeGuru supports **JAVA**.
Repository can use **GitHub** or **CodeCommit**. It is also easy to integrate.


![codeguru](/images/codequeility.png)

CodeGuru's service is composed of two types. 

### 1. CodeGuru Reviewer that provides Automated CodeReview
  Amazon CodeGuru Reviewer finds issues in your code and recommends how to remediate them.

  ![codegurureviewer](/images/git-pr-codereviewer.png) 

   The contents that CodeGuru Reviewer detects can be this categories.
  1. AWS Best Practices : AWS APIs contain a rich set of features to ensure performance and stability of software.
  1. Concurrency : CodeGuru Reviewer identifies problems with implementations of concurrency in multithreaded code
  1. Resource Leaks : CodeGuru Reviewer looks for lines of code where resource leaks might be occurring.
  1. Sensitive Information Leak : Sensitive information in code should not be shared with unauthorized parties..

### 2. CodeGuru Profiler

  Amazon CodeGuru Profiler is always searching for application performance optimizations, identifying your most **expensive** lines of code and recommending ways to fix them to reduce CPU utilization, cut compute costs, and improve application performance. 

- [Now let`s get ready for the this lab.](/en/setup/)
