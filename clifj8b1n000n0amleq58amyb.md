---
title: ".NET Core CI/CD Pipeline using GitHub Action Workflow"
datePublished: Sat Jun 03 2023 05:07:00 GMT+0000 (Coordinated Universal Time)
cuid: clifj8b1n000n0amleq58amyb
slug: net-core-cicd-pipeline-using-github-action-workflow
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1685768776049/40d53fac-0142-411c-8a82-701dbd6c35bc.png
tags: aws, web-development, developer, devops, beginners

---

# 🚀 Introduction

In this tutorial, we will dive into the process of setting up a CI/CD pipeline for a .NET Core application using .NET SDK and Ubuntu Server, and deploying to AWS Elastic Beanstalk using GitHub Actions. This pipeline will enable you to automate the build, test, and deployment processes, ensuring a smooth and efficient development workflow. We will walk through creating a GitHub repository for the application, setting up a GitHub Actions workflow to build and publish the application using .NET SDK, and deploying the package to AWS Elastic Beanstalk. Let's get started!

### 🔧 Prerequisites

Before we begin, make sure you have the following:

1. An AWS account: You will need an AWS account to create and manage the necessary resources for deployment.
    
2. An Ubuntu Server instance on AWS EC2: This instance will be used to run the build and deployment processes.
    
3. .NET SDK and AWS CLI installed on the Ubuntu Server instance: These tools are required to build and deploy the application.
    
4. A .NET Core application created using Visual Studio or the dotnet new command: This is the application you will be building and deploying.
    

### 📝 Step-by-Step Guide

1. Create a GitHub repository for the application and push the code to the repository.
    

Start by creating a GitHub repository for your .NET Core application. Once the repository is created, clone it to your local machine, add your application code, and push the changes to the repository.

1. Set up a GitHub Actions workflow to build and publish the application using .NET SDK.
    

Next, create a GitHub Actions workflow file in your repository (e.g., **.github/workflows/ci-cd.yml**). This file will define the steps to build, publish, and deploy your application using .NET SDK and AWS Elastic Beanstalk. Here's an example workflow file:

```plaintext
name: Build and Publish

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v2

    - name: Setup .NET SDK
      uses: actions/setup-dotnet@v1
      with:
        dotnet-version: '5.0.x'

    - name: Restore dependencies
      run: dotnet restore

    - name: Build
      run: dotnet build --configuration Release --no-restore

    - name: Test
      run: dotnet test --no-restore --verbosity normal

    - name: Publish
      run: dotnet publish -c Release -o ./publish

    - name: Deploy to AWS Elastic Beanstalk
      uses: einaregilsson/beanstalk-deploy@v16
      with:
        aws_access_key: ${{ secrets.AWS_ACCESS_KEY }}
        aws_secret_key: ${{ secrets.AWS_SECRET_KEY }}
        region: us-east-1
        application_name: my-application
        environment_name: my-environment
        version_label: ${{ github.sha }}
        package: ./publish
```

1. Set up the necessary AWS resources, including an Elastic Beanstalk application and environment, and configure the environment to use the appropriate platform and instance type.
    

Create an Elastic Beanstalk application and environment using the AWS Management Console or the AWS CLI. Configure the environment to use the appropriate platform (e.g., .NET Core on Linux) and instance type (e.g., t2.micro).

1. Create AWS IAM credentials with sufficient permissions to deploy the application to Elastic Beanstalk, and store the credentials as GitHub secrets.
    

Using the AWS Management Console or the AWS CLI, create an IAM user with the necessary permissions to deploy the application to Elastic Beanstalk. Then, store the IAM user's access key and secret key as GitHub secrets in your repository (e.g., **AWS\_ACCESS\_KEY** and **AWS\_SECRET\_KEY**).

1. Test the workflow by pushing changes to the repository and verifying that the application is deployed to Elastic Beanstalk.
    

Make changes to your application code, commit the changes, and push them to the repository. GitHub Actions will automatically trigger the workflow, and the application will be built, published, and deployed to Elastic Beanstalk.

# 🎉 Conclusion

Congratulations! You have successfully set up a CI/CD pipeline for a .NET Core application using .NET SDK and Ubuntu Server, and deploying to AWS Elastic Beanstalk using GitHub Actions. With this pipeline in place, you can easily build, test, and deploy your application with confidence, ensuring a smooth and efficient development workflow.

### **📢 Resource:** [3 Ways to install .NET Core (dotnet) on Ubuntu 20.04 LTS Focal fossa](https://www.google.com/url?sa=i&url=https%3A%2F%2Flinux.how2shout.com%2F3-ways-to-install-net-6-dotnet-on-ubuntu-20-04-lts-focal-fossa%2F&psig=AOvVaw3MNbc0NAvvXtWTfIa7uBXt&ust=1685855105743000&source=images&cd=vfe&ved=0CBMQjhxqFwoTCPiWqeippv8CFQAAAAAdAAAAABAE)

## 👉 **Checkout GitHub Repository for projects:**

**🔗** [**github.com/sumanprasad007**](http://github.com/sumanprasad007)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685557869584/83798879-b1f8-4857-b884-f8c2ef3213a2.png?auto=compress,format&format=webp align="left")