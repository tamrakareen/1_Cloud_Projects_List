![placeholder image](https://cloudysave-new.b-cdn.net/wp-content/uploads/2020/07/Terraform-AWS-RDS-Terraform-Logo.jpg)

Deploying a VM in AWS using Terraform Workflow

## Introduction

Terraform is an infrastructure as code (IaC) tool that allows you to build, change, and version infrastructure safely and efficiently. You can use a consistent workflow to provision and manage all of your infrastructure throughout its lifecycle. Terraform can manage low-level components like compute, storage, and networking resources, as well as high-level components like DNS entries and SaaS features. This practicioner level project will focus on creating compute resources through AWS.

## Prerequisite

A Cloud Guru Account OR AWS account AND Terraform 

## Cloud Research

When I started this project, I wanted to install Terraform and use my own AWS account, but Terraform was not installing correctly on my windows laptop.  I used powershell to install Chocolatey and install Terraform that way, but still no luck.  Thankfully I have access to A Cloud Guru's playgound and can use their instant terminals. I was able to open a Terraform terminal from their website and get started. 

### Step 1 — Understanding The Core Terraform Workflow

![placeholder image](https://www.devopsschool.com/blog/wp-content/uploads/2019/10/Terraform-Basics-Workflow.png)

The core Terraform workflow consists of three stages:

Write: You define resources, which may be across multiple cloud providers and services. For example, you might create a configuration to deploy an application on virtual machines in a Virtual Private Cloud (VPC) network with security groups and a load balancer.

Plan: Terraform creates an execution plan describing the infrastructure it will create, update, or destroy based on the existing infrastructure and your configuration.

Apply: On approval, Terraform performs the proposed operations in the correct order, respecting any resource dependencies. For example, if you update the properties of a VPC and change the number of virtual machines in that VPC, Terraform will recreate the VPC before scaling the virtual machines.

In short:

Write- Create your Terraform code 

Plan- Add and review changes to code 

Apply- Deploy infrastructure

### Step 2 — (Write) Create a Directory and Write Your Terraform Code 

First I logged into the AWS Management Console with the provided username and password. I created a new directory to house my Terraform code. I created a new file called main.tf. To create my EC2 instance (VM) in AWS, I used this code:

provider "aws" {

  region = "us-east-1"
  
}

resource "aws_instance" "vm" {

  ami           = "DUMMY_VALUE_AMI_ID"
  
  subnet_id     = "DUMMY_VALUE_SUBNET_ID"
  
  instance_type = "t3.micro"
  
  tags = {
  
    Name = "my-first-tf-node"
    
  }
  
![Screenshot](https://static.wixstatic.com/media/ace974_121cc666fdd3433481199512ae8ee1da~mv2.png/v1/fill/w_740,h_416,al_c,q_90/ace974_121cc666fdd3433481199512ae8ee1da~mv2.webp)

![Screenshot](https://static.wixstatic.com/media/ace974_0a1a7070c50f4de08fb84939133d1719~mv2.jpg/v1/fill/w_740,h_297,al_c,q_90/ace974_0a1a7070c50f4de08fb84939133d1719~mv2.webp)

![Screenshot](https://static.wixstatic.com/media/ace974_3ea48b50a1874d2e882f0f6ddab6a24a~mv2.png/v1/fill/w_740,h_358,al_c,q_90/ace974_3ea48b50a1874d2e882f0f6ddab6a24a~mv2.webp)

### Step 3 — Plug the AMI and SUBNET ID Values Into Your Code

The Amazon Machine Image and subnet ID were provided for me.

![Screenshot](https://static.wixstatic.com/media/ace974_2137dc388aec4769930a8f45624f84f3~mv2.png/v1/fill/w_740,h_304,al_c,q_90/ace974_2137dc388aec4769930a8f45624f84f3~mv2.webp)

![Screenshot](https://static.wixstatic.com/media/ace974_847fe7447e444c8385371dc122fd0cf7~mv2.png/v1/fill/w_740,h_319,al_c,q_90/ace974_847fe7447e444c8385371dc122fd0cf7~mv2.webp)

### Step 4 — (Plan) Initialize and Review Your Terraform Code 

I used the code Terraform init to initialize the configuration and Terraform plan to review sthe actions that will be performed when the code is deployed.

![Screenshot](https://static.wixstatic.com/media/ace974_121cc666fdd3433481199512ae8ee1da~mv2.png/v1/fill/w_740,h_416,al_c,q_90/ace974_121cc666fdd3433481199512ae8ee1da~mv2.webp) 

![Screenshot](https://static.wixstatic.com/media/ace974_7766f61eb70e4420a2b41a54c4039a6d~mv2.png/v1/fill/w_740,h_422,al_c,q_90/ace974_7766f61eb70e4420a2b41a54c4039a6d~mv2.webp)

![Screenshot](https://static.wixstatic.com/media/ace974_3e7257f7e7534fbcb5ba736e5f0faf9e~mv2.png/v1/fill/w_740,h_416,al_c,q_90/ace974_3e7257f7e7534fbcb5ba736e5f0faf9e~mv2.webp)

### Step 5 — (Apply) Deploy Your Terraform Code, Verify Resources, and Destroy

I deployed the infrastructure with Terraform apply.

![Screenshot](https://static.wixstatic.com/media/ace974_5e7cee9f24864250ab23aeb2fe6ba53f~mv2.png/v1/fill/w_740,h_426,al_c,q_90/ace974_5e7cee9f24864250ab23aeb2fe6ba53f~mv2.webp)

![Screenshot](https://static.wixstatic.com/media/ace974_e2372330fb424974aa3a75fb2f87e4b8~mv2.png/v1/fill/w_740,h_415,al_c,q_90/ace974_e2372330fb424974aa3a75fb2f87e4b8~mv2.webp)

I verified that my resource was created from the AWS console.

![Screenshot](https://static.wixstatic.com/media/ace974_fdc68edb3f2d4a84843ccd3ccbf52c6b~mv2.png/v1/fill/w_740,h_425,al_c,q_90/ace974_fdc68edb3f2d4a84843ccd3ccbf52c6b~mv2.webp)

![Screenshot](https://static.wixstatic.com/media/ace974_79088b80bc694132a42188898685ed18~mv2.png/v1/fill/w_740,h_406,al_c,q_90/ace974_79088b80bc694132a42188898685ed18~mv2.webp)

And finally, I took down the infrastructure with the Terraform destroy command.

![Screenshot](https://static.wixstatic.com/media/ace974_2fdf0330df324390bb04df6d3e95b5ae~mv2.png/v1/fill/w_740,h_416,al_c,q_90/ace974_2fdf0330df324390bb04df6d3e95b5ae~mv2.webp)

![Screenshot](https://static.wixstatic.com/media/ace974_8c2316638c2c4f7eb726e05364f1df11~mv2.png/v1/fill/w_740,h_416,al_c,q_90/ace974_8c2316638c2c4f7eb726e05364f1df11~mv2.webp)

## ☁️ Cloud Outcome

✍️ I liked this project, it was simple and jogged my memory of learning Terraform. This would be a really fast process if I had to spin up a bunch of vm's.

## Next Steps

Next I'd like to build and test a Terraform module.

