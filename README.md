# ![aws](https://github.com/julien-muke/Search-Engine-Website-using-AWS/assets/110755734/01cd6124-8014-4baa-a5fe-bd227844d263) End-to-End CI/CD Pipeline for Node.js Web Application using AWS.


## <a name="introduction">🤖 Introduction</a>

AWS CodePipeline is a fully managed continuous delivery service that helps you automate your release pipelines for fast and reliable application and infrastructure updates.

In this demo, we are going to learn how to build a CI/CD pipeline for a Node.js web application using AWS CI/CD services (CodeBuild, CodeDeploy, CodePipeline). We will start from scratch and proceed to the end. First, we will explore the architecture, and then we will build the pipeline.


## <a name="design">📐 Architecture Diagram</a>

![CD:CD Pipeline](https://github.com/julien-muke/aws-cicd-devops-web-app/assets/110755734/2c83b581-36ae-4464-ae64-3be22531cb43)

## Architecture overview

The architecture of the CI/CD pipeline is as follows: Users start by pushing a new commit to the GitHub repository. This triggers the pipeline, which consists of three stages: Source, Build, and Deploy. The Source stage pulls the source code from the GitHub repository. The Build stage uses AWS CodeBuild to Test the Node.js web application. The Deploy stage uses AWS CodeDeploy to deploy the Node.js web application to an Elaastic Beanstalk environment.

## <a name="steps">☑️ Steps</a>

The procedure for deploying this architecture on AWS consists of the following steps:

Step 1: Create a Instance role Elastic Beanstalk

Step 2: Creating an Elastic Beanstalk environment

Step 3: Create a Pipeline to Deploy Node.js Application


##  	:octocat: Clone example repository

Clone the [example repository](https://github.com/julien-muke/aws-cicd-devops-web-app-sample.git) for this tutorial, which contains the Node.js Application.

```bash
git clone https://github.com/julien-muke/aws-cicd-devops-web-app-sample.git
```

Change into the repository directory.

```bash
cd aws-cicd-devops-web-app-sample
```

## ➡️ Step 1 - Create a Instance role Elastic Beanstalk

An instance profile is a container for an AWS Identity and Access Management (IAM) role that you can use to pass role information to an Amazon EC2 instance when the instance starts.

If your AWS account doesn’t have an EC2 instance profile, you must create one using the IAM service. You can then assign the EC2 instance profile to new environments that you create. The Create environment wizard provides information to guide you through the IAM service, so that you can create an EC2 instance profile with the required permissions. After creating the instance profile, you can return to the console to select it as the EC2 instance profile and continue the steps to create your environment.

To create an instance profile:

1. Open the [Roles](https://console.aws.amazon.com/iam/home#roles) page in the IAM console.
2. Choose Create role.

![1](https://github.com/julien-muke/aws-cicd-devops-web-app/assets/110755734/369f4232-4220-4adc-931e-53ab3c939524)


3. Under Trusted entity type, choose AWS service.
4. Under Use case, choose EC2.
5. Choose Next.

![2](https://github.com/julien-muke/aws-cicd-devops-web-app/assets/110755734/fa9def89-ae17-4055-a1fd-9155519702f3)


6. Attach the appropriate managed policies provided by Elastic Beanstalk and any additional policies that provide permissions that your application needs.
7. Choose Next.
8. Enter a name for the role.
9. Choose Create role.

![4](https://github.com/julien-muke/aws-cicd-devops-web-app/assets/110755734/589744dc-3fed-4796-aa45-c09edfe77e71)


## ➡️ Step 1 - Creating an Elastic Beanstalk environment

An AWS Elastic Beanstalk environment is a collection of AWS resources running an application version. You can deploy multiple environments when you need to run multiple versions of an application. For example, you might have development, integration, and production environments.

To launch an environment with a sample application (console):

1. Open the [Elastic Beanstalk console](https://console.aws.amazon.com/elasticbeanstalk), and in the Regions list, select your AWS Region.
2. In the navigation pane, choose Applications, and then choose create application.

![Screenshot 2024-07-08 at 11 51 35](https://github.com/julien-muke/aws-cicd-devops-web-app/assets/110755734/bae0b96a-52c4-4270-9153-90848dec5fcb)


3. On the application overview page, choose Create new environment.

![Screenshot 2024-07-08 at 11 52 01](https://github.com/julien-muke/aws-cicd-devops-web-app/assets/110755734/dc8e3bb8-97ed-48bc-96ea-cd71018a712b)

This launches the Create environment wizard. The wizard provides a set of steps for you to create a new environment.

4. For environment tier, choose the Web server environment.

![Configure-environment-Elastic-Beanstalk-us-east-1](https://github.com/julien-muke/aws-cicd-devops-web-app/assets/110755734/1dc57ce3-008b-4988-ad20-1b195645096d)


5. For Platform, select the platform and platform branch that match the language your application uses, in my case it's `Node.js`
6. For Application code, choose Sample application.
7. For Configuration presets, choose Single instance.
8. Choose Next.


![Configure-environment-Elastic-Beanstalk-us-east-1 copy](https://github.com/julien-muke/aws-cicd-devops-web-app/assets/110755734/af4124ec-fd7e-448a-890c-917f63d68bb2)


9. Choose Use an existing service role for Service Role.
10. Next, we'll focus on the EC2 instance profile dropdown list. The values displayed in this dropdown list may vary, depending on whether you account has previously created a new environment.

Choose one of the following, based on the values displayed in your list:
* If `aws-elasticbeanstalk-ec2-role` displays in the dropdown list, select it from the EC2 instance profile dropdown list.
* If another value displays in the list, and it’s the default EC2 instance profile intended for your environments, select it from the EC2 instance profile dropdown list `aws-cicd-web-app-role`.
* If the EC2 instance profile dropdown list doesn't list any values to choose from, expand the procedure that follows, Create IAM Role for EC2 instance profile.

11. Choose Next.
12. Review configuration then choose Next.

![Screenshot 2024-07-08 at 11 55 14](https://github.com/julien-muke/aws-cicd-devops-web-app/assets/110755734/29e489af-d737-4501-b6c9-2b8ab10c5b7e)

13. The Elastic Beanstalk Environment will take few munites to launch.
14. Once the environment is successfully launched, click on the URL Domain to test the application.

![Screenshot 2024-07-08 at 12 05 44](https://github.com/julien-muke/aws-cicd-devops-web-app/assets/110755734/e0de67eb-0a0d-4a70-b9b1-c601be0f85ca)


![Screenshot 2024-07-08 at 12 07 22](https://github.com/julien-muke/aws-cicd-devops-web-app/assets/110755734/f782c6c2-bb2d-4b6f-8587-2519370ce0f0)
