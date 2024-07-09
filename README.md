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


## ➡️ Step 2 - Creating an Elastic Beanstalk environment

An AWS Elastic Beanstalk environment is a collection of AWS resources running an application version. You can deploy multiple environments when you need to run multiple versions of an application. For example, you might have development, integration, and production environments.

To launch an environment with a sample application (console):

1. Open the [Elastic Beanstalk console](https://console.aws.amazon.com/elasticbeanstalk), and in the Regions list, select your AWS Region.
2. In the navigation pane, choose Applications, and then choose create application, name your app `My-First-App`.

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


## ➡️ Step 3 - Create a Pipeline to Deploy Node.js Application


To create a pipeline in the console, you must provide the source file location and information about the providers you will use for your actions.

We will create a pipeline to deploy the Node.js web application to an Elastic Beanstalk environment. We will use AWS CodePipeline to create a pipeline that automates the deployment process.

To create a pipeline in the console:

1. Open the CodePipeline console at http://console.aws.amazon.com/codesuite/codepipeline/home.
2. On the Welcome page, choose Create pipeline. 


![Screenshot 2024-07-08 at 12 52 40](https://github.com/julien-muke/aws-cicd-devops-web-app/assets/110755734/09598a4d-e20a-4813-b209-6805a72e17e8)


3. Choose pipeline settings page, in Pipeline name, enter the name for your pipeline `devops-web-app-pipeline`
4. In Execution mode, choose Queued (Pipeline type V2 required)
5. In Service role, Choose New service role to allow CodePipeline to create a new service role in IAM.
6. Choose Next.

![Create-new-pipeline-CodePipeline-us-east-1(5)](https://github.com/julien-muke/aws-cicd-devops-web-app/assets/110755734/fdaa5179-5a25-436e-bdcb-32ec5b9c1313)


7. Add source stage page, in Source provider, choose the type of repository where your source code is stored, specify its required options, in my case i will choose GitHub (Version 2).

* Under Connection, choose an existing connection or create a new one. To create or manage a connection for your GitHub source action, see [GitHub connections](https://docs.aws.amazon.com/codepipeline/latest/userguide/connections-github.html). 

![Screenshot 2024-07-08 at 13 07 23](https://github.com/julien-muke/aws-cicd-devops-web-app/assets/110755734/7ba93582-d6ef-4a65-a1ee-80cba63506ab)

* Choose the repository you want to use as the source location for your pipeline. 

![Screenshot 2024-07-08 at 13 08 40](https://github.com/julien-muke/aws-cicd-devops-web-app/assets/110755734/bc420b03-868d-4df9-ae16-95ac676972c1)


* GitHub Apps create a link for your connection with GitHub. To start, install a new app and
save this connection.

![Screenshot 2024-07-08 at 13 09 36](https://github.com/julien-muke/aws-cicd-devops-web-app/assets/110755734/7aea793a-1464-461a-9e22-b81a4864133f)


* Select your GitHub repository `julien-muke/aws-cicd-devops-web-app-sample`

![Screenshot 2024-07-08 at 13 11 38](https://github.com/julien-muke/aws-cicd-devops-web-app/assets/110755734/b54dc28e-65c5-4fa8-b250-5e4531f69b01)


* Choose again a repository in your GitHub Account, then choose `main` as default branch
* Enter `main` branch to trigger the pipeline, then choose Next.

![Create-new-pipeline-CodePipeline-us-east-1(6)](https://github.com/julien-muke/aws-cicd-devops-web-app/assets/110755734/6895bea7-3346-481b-aec5-6cbc0c20883f)


7. On the Add build stage page, From Build provider, choose a custom action provider of build services, and provide the configuration details for that provider, choose `AWS CodeBuild`

8. In Project name, choose your build project. If you have already created a build project in CodeBuild, choose it. Or you can create a build project in CodeBuild and then return to this task. Follow the instructions in Create a Pipeline That Uses CodeBuild in the CodeBuild User Guide.

* Choose Create project

![Screenshot 2024-07-08 at 13 17 46](https://github.com/julien-muke/aws-cicd-devops-web-app/assets/110755734/64568078-a3ce-4a66-a790-c2c43d8188ca)


* Enter the Project name `devops-web-app`

![Screenshot 2024-07-08 at 13 19 05](https://github.com/julien-muke/aws-cicd-devops-web-app/assets/110755734/f78d5c46-7f5a-4f93-aa70-d43e4d72113d)


* Under Build specifications, choose Use a buildspec file to Store build commands in a YAML-formatted buildspec file.

![Screenshot 2024-07-08 at 13 20 01](https://github.com/julien-muke/aws-cicd-devops-web-app/assets/110755734/6a05ce71-bd22-43d9-9291-b924ee276050)


* Scroll down and Choose Continue to CodePipeline.

* Once the is created, go back to the build page, and choose Next.

9. On the Add deploy stage page, In Deploy provider, choose a custom action that you have created for a deployment provider which is `AWS Elastic Beanstalk`

10. In Application name, enter or choose the name of an existing Elastic Beanstalk application `My-First-App`
11. n Environment name, enter an environment for the application `My-First-App-env`. Choose Next.


![Screenshot 2024-07-08 at 14 25 05](https://github.com/julien-muke/aws-cicd-devops-web-app/assets/110755734/a81c01fa-4635-46c7-a205-4313474e50e6)


12. Review page, review your pipeline configuration, and then choose Create pipeline.


Note: The Pipeline will be triggered automatically. But we need to modify one setting to run the Pipeline Successfully. Since we are not building any Binaries or Docker Images, we are not using BuildArtifacts Option. So we also need to update that setting in Deploy Stage.

Artifacts are the files that are worked on by actions in the pipeline. See the action configuration for each action for details about artifact parameters. For example, the S3 source action artifact is a file name (or file path), and the files are generally provided as a ZIP file.


13. Let's edit the pipiline, in the codePipeline console, click Edit

![Screenshot 2024-07-08 at 14 28 01](https://github.com/julien-muke/aws-cicd-devops-web-app/assets/110755734/6f7765d7-aa63-4e67-bdca-316dd225af84)


14. Scroll down to Edit: Deploy and choose Edit stage.

![Screenshot 2024-07-08 at 14 28 16](https://github.com/julien-muke/aws-cicd-devops-web-app/assets/110755734/e9f4851e-af86-4b20-aef9-42cd68e295ed)


15. Click on the edit icon

![Screenshot 2024-07-08 at 14 28 24](https://github.com/julien-muke/aws-cicd-devops-web-app/assets/110755734/f61aeeca-f6b0-49fb-9faf-97966c0c9d21)


16. Under Input artifacts, choose `SourceArtifacts`

![Screenshot 2024-07-08 at 14 28 36](https://github.com/julien-muke/aws-cicd-devops-web-app/assets/110755734/5f8e2b90-5aea-4bfd-a9d1-48dc6a4b9242)


17. Back to CodePipeline console, choose Save


![Screenshot 2024-07-08 at 14 29 00](https://github.com/julien-muke/aws-cicd-devops-web-app/assets/110755734/210e933c-48d8-4294-864b-ae2bd668a3e3)

Note: If You are not changing the BuildArtifact to SourceArtifact, you’ll run into some errors, make sure to edit the input artifacts to SourceArtifact as shown above.

Now, let's trigger the Pipeline by making a Changes in Respository.

1. For example, i'll open GitHub Respository, and edit the title by adding 2024 at the end of the title.
2. Then click Commit changes.

![Screenshot 2024-07-08 at 14 52 57](https://github.com/julien-muke/aws-cicd-devops-web-app/assets/110755734/c703b944-4f0c-4c9e-ae8b-b1f427cd5109)


3. 



