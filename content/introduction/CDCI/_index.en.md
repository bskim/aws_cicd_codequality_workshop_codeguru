---
title: "CI/CD with Code Series"
weight: 11
pre: "<b>1-1 </b>"
tag:
  - Code Series
---

## Waht is CI/CD?(Continuous Integration/Continuous Delivery)


CI / CD is a way to automate build and test to deliver applications to customers in shorter cycles.
It is also a solution to solve various problems caused by the merge of idff codes that developers change. CI/CD primarily refers to the build or integration phase during the software release process, and provides automation and monitoring throughout the application lifecycle.

![AWSPipeline](/images/continuous_integration.4f4cddb8556e2b1a0ca0872ace4d5fe2f68bbc58.png)

**CI** (Continuous Deployment) means that changes from developers are automatically uploaded to **Repository** after bug testing.
**CD** (Continuous Deployment) means that the developer's changes are all tested and automatically released to the production environment delivery to the customer.
As a result, CI/CD means the actual process represented by the pipeline and adds automation monitoring of application development. 

This allows developers to test their code with minimal effort, or even to actual release. For this reason, a well-formed CI/CD pipeline can improve code quality due to automated tests set on the pipeline, while speeding up the development cycle and improving overall development speed.


## How? What should I use?

You can use the **AWS ode Series**. Code series is a fully managed service, so there is no need for a infrastructure.
![codeseries](/images/codeseries.svg)

1. **CodeCommit**: AWS CodeCommit is a fully-managed source control service that hosts secure Git-based repositories.
1. **CodeBuild**: AWS CodeBuild is a fully managed continuous integration service that compiles source code, runs tests, and produces software packages that are ready to deploy.
1. **CodeDeploy**: AWS CodeDeploy is a fully managed deployment service that automates software deployments to a variety of compute services such as Amazon EC2, AWS Fargate, AWS Lambda, and your on-premises servers. 
1. **CodePipeline**: AWS CodePipeline is a fully managed continuous delivery service that helps you automate your release pipelines for fast and reliable application and infrastructure updates.
 
-[ and.. What is UnitTest? ](/en/introduction/unittest)

