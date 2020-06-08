---
title: "CloudFormation"
weight: 21
pre: "<b>2-0. </b>"
---

## AWS Account
{{% notice warning %}}
If you already have an AWS account, you can immediately follow the this lab, but **If you don't have an account**, you need to create an AWS account first.
{{% /notice %}}
For an AWS account creation and activation guide, visit this link [link](https://aws.amazon.com/en/premiumsupport/knowledge-center/create-and-activate-aws-account/)

{{% notice info %}}
For practice, select **us-west-2 (Oregon) region**. This lab **will not work in other AWS Regions**
Before starting this lab, the resources required for this lab are configured using AWS CloudFormation, and then CodeGuru and Codebuild Report are configured.
{{% /notice %}}

## IAM User
If you have created an AWS account but have not created an IAM user, you can create an IAM user using the IAM console. Follow the steps below to create an Administrator user. If you already have an admin user, skip the next IAM user creation task.


1. Sign in to the [IAM Console](https://console.aws.amazon.com/iam/) as the **Root** user in your AWS account using your AWS account email address and password.
1. Select **Users** from the menu panel on the left side of the IAM console, then click **Add user**.
1. Enter **User name** as `Administrator`.
1. Select the **AWS Management Console access** checkbox, select **Custom password**, and enter your password.
1. Click **Next: Permissions**.

![IAMPermission](/images/iam_user_01.png)
1. Select **Attach existing policies directly**, select the checkbox for the **AdministratorAccess** policy, and click **Next: Tags**.

![IAMPolicy](/images/iam_user_02.png)
1. Click **Next: Review**.
1. Verify that the AdministratorAccess managed policy has been added to the Administrator user, and click **Create user**.
1. Now, **logout** the user **logout** and **login** as the newly created **Administrator** user. You can log in using the following URL:
> `https://<your_aws_account_id>.signin.aws.amazon.com/console/`  
{{% notice warning %}}
<your_aws_account_id> is the unique ID of your AWS account. As a root user, an error may occur when performing this exercise.
{{% /notice %}}

## EC2 Key Pair
To configure the basic environment required for the lab using the CloudFormaton template, you must provide an Amazon EC2 key pair. If you already have an EC2 key pair, **skip the next task**.
1. Sign in to the AWS console as a **Administrator** user, and then go to the EC2 Console (https://console.aws.amazon.com/ec2/).
1. In the navigation pane, select **Key Pairs** from **Network & Security**.
1. Click **Create Key Pair**.
1. Enter the name of the new key pair in **Key pair name**, then click **Create**.
1. Private Key file in .PEM file format is automatically downloaded from the browser. The private key is required when using the following CloudFormation.

## CloudFormation Template
Create a CloudFormation stack using the CloudFormation-template provided to proactively create the AWS resources needed for the AWS AWS CodeQuality lab.
Create EC2 and VPC for development and production environments, and CodePipeline, CodeBuild, CodeDeploy, and CodeCommit to live in each environment.

To launch the CloudFormation stack, click the  [Launch Stack button](https://console.aws.amazon.com/cloudformation/home?region=us-west-2#/stacks/new?stackName=CodeQuality-Workshop&templateURL=https://sykang-productionapp.s3-us-west-2.amazonaws.com/vpc.template) to go to the CloudFormation console.

{{% notice warning %}}
Important: This template was created for us-west-2 (Oregon) and does not work in other AWS Regions.
{{% /notice %}}

{{% button href="https://console.aws.amazon.com/cloudformation/home?region=us-west-2#/stacks/new?stackName=CodeQuality-Workshop&templateURL=https://sykang-productionapp.s3-us-west-2.amazonaws.com/vpc.template" icon="fab fa-aws" icon-position="left" %}}&nbsp;Launch Stack{{% /button %}}

In the stack creation step, enter a stack name and choose the EC2 key pair you created before. And in the final step, select **Acknowledge checkbox** and click **Create stack** so that CloudFormation can use a custom name when creating the IAM resource.

![CloudFormation_01](/images/cloudformation-specify-stack-details.png)
It takes about 5 minutes to complete the CloudFormation stack. Check the CloudFormation console and wait for the **CREATE_COMPLETE** status as shown below.
![CloudFormation_03](/images/cloudformation-stacks-info.png)
{{% notice note %}}
When the stack creation is complete, your AWS account has all the basic resources needed to run the lab. **Outputs** tab, the name of **DevWebApp01** and the name of **ProudWebApp01** are displayed.
{{% /notice %}}

-[Now let`s build the CI/CD pipeline in the created build environment.](/en/setup/cloud9) 



