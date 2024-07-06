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

Step 2: Configure Elastic Beanstalk Environment

Step 3: Create a Pipeline to Deploy Node.js Application


##  	:octocat: Clone example repository

Clone the [example repository](https://github.com/julien-muke/aws-cicd-devops-web-app-sample.git) for this tutorial, which contains configuration for an Auto Scaling group.

```bash
git clone https://github.com/julien-muke/aws-cicd-devops-web-app-sample.git
```

Change into the repository directory.

```bash
cd aws-cicd-devops-web-app-sample
```

## ➡️ Step 1 - Create a Instance role Elastic Beanstalk

