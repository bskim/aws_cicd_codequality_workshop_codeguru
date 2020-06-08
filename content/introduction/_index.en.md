---
title: "Introduction"
weight: 10
pre: "<b>1. </b>"
tag:
  - Pipeline
  - CodeCommit
  - CodeBuild
  - CodeDeploy
  - CI/CD
  - UnitTest
---

{{% notice note %}}
If you know the concept and CI/CD and CodeSeries, junp to [Step 2 (lab environment)](/setup).
{{% /notice%}}

 ![problem0](/images/gitbranchenv2.svg)


|Name|contents|
|---|---|
| **master** | Production Code or Production-ready Code |
| **develop** | Integration Branch, development progress|


The lab environment consists of two branches, `master` and `develop`.
Each branch consists of a build and deployment environment using **Code Pipeline**. Growing to the develop branch commit are immediately deploying to the `development environment`, while grow to master branch commit are immediately deploying to the production environment.

 ![problem0](/images/gitbranch3.svg)

Therefore, the `code review` and `unit test` results is very important when merging to master branch. This should be able to be immediately delivered to the developer.

This lab covers visualizing the results of the automated **unit test** with CodeBuild when diff in develop are merged into master. And using **CodeGuru** to show you how to code review automated in pull-request.

- [Now, I will explain the concepts of CI/CD and the services to be used in the lab.](/en/introduction/cdci)
 