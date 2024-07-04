# ![aws](https://github.com/julien-muke/Search-Engine-Website-using-AWS/assets/110755734/01cd6124-8014-4baa-a5fe-bd227844d263) End-to-End CI/CD Pipeline for Node.js Web Application using AWS.


## <a name="introduction">🤖 Introduction</a>

AWS CodePipeline is a fully managed continuous delivery service that helps you automate your release pipelines for fast and reliable application and infrastructure updates.

In this demo, we are going to learn how to build a CI/CD pipeline for a Node.js web application using AWS CI/CD services (CodeBuild, CodeDeploy, CodePipeline). We will start from scratch and proceed to the end. First, we will explore the architecture, and then we will build the pipeline.


## <a name="design">📐 Architecture Diagram</a>

![ECS Terraform](https://github.com/julien-muke/ec2-auto-scaling-terraform/assets/110755734/7b028d20-dbbe-4228-883f-2eb9a2851095)


## <a name="steps">☑️ Steps</a>

The procedure for deploying this architecture on AWS consists of the following steps:

* Create a VPC, Subnets, and Configure network requirements.
* Create EC2 instances with Auto scaling group and Launch template.
* Create a Load balancer with a target group to the Auto Scaling group.


## 📝 Prerequisites

This tutorial assumes that you are familiar with the standard Terraform workflow. If you are new to Terraform, complete the [Get Started tutorials](https://developer.hashicorp.com/terraform/tutorials/aws-get-started) first.

For this tutorial, you will need:

* [Terraform v1.8+ installed locally](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli).
    
* An [AWS account](https://portal.aws.amazon.com/billing/signup) with [credentials configured for Terraform](https://registry.terraform.io/providers/hashicorp/aws/latest/docs#authentication).
    
* The [AWS CLI](https://aws.amazon.com/cli/)

##  	:octocat: Clone example repository

Clone the [example repository](https://github.com/julien-muke/learn-terraform-aws-asg) for this tutorial, which contains configuration for an Auto Scaling group.

```bash
git clone https://github.com/julien-muke/learn-terraform-aws-asg.git
```

Change into the repository directory.

```bash
cd learn-terraform-aws-asg
```
