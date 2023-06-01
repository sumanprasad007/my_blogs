---
title: "CI/CD Pipeline for .NET Standard Framework Application using GitHub Action"
datePublished: Thu Jun 01 2023 03:56:50 GMT+0000 (Coordinated Universal Time)
cuid: cliclucky00080amh1n5hcxce
slug: cicd-pipeline-for-net-standard-framework-application-using-github-action
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1685591712372/b51e7728-df1d-47a7-a1bb-d2de9ed4422a.png
tags: aws, web-development, developer, devops, beginners

---

# 🚀 Introduction

In this tutorial, we will learn how to set up a CI/CD pipeline for a .NET Standard application using MSBuild, Windows Server, AWS Beanstalk, and GitHub Actions. We will create a GitHub repository for the application, set up a GitHub Actions workflow to build and publish the application using MSBuild, and deploy the package to AWS Beanstalk. Let's get started!

### 🔧 Prerequisites Before we begin, make sure you have the following:

* An AWS account
    
* A Windows Server instance on AWS EC2
    
* MSBuild, .NET Core SDK, and AWS CLI installed on the Windows Server instance
    
* A .NET Standard application created using Visual Studio or the **dotnet new** command
    

### 📝 Step-by-Step Guide

1. Configure the application to use MSBuild for building and publishing the project. Add a [**Directory.Build**](http://Directory.Build)**.props** file to the project directory with the following contents:
    

```plaintext
<Project>
  <PropertyGroup>
    <PublishDir>$(MSBuildProjectDirectory)\publish</PublishDir>
  </PropertyGroup>
</Project>
```

1. Create a GitHub repository for the application and push the code to the repository.
    
2. Set up a GitHub Actions workflow to build and publish the application using MSBuild. Here's an example workflow file:
    

```plaintext
name: Build and Publish

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: windows-latest

    steps:
    - uses: actions/checkout@v2

    - name: Setup MSBuild
      uses: microsoft/setup-msbuild@v1.0.2

    - name: Build and Publish
      run: msbuild /t:Publish /p:Configuration=Release

    - name: Deploy to AWSstalk
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
    
2. Create AWS IAM credentials with sufficient permissions to deploy the application to Beanstalk, and store the credentials as GitHub secrets.
    
3. Test the workflow by pushing changes to the repository and verifying that the application is deployed to Beanstalk.
    

# 🎉 Conclusion

Congratulations! You have successfully set up a CI/CD pipeline for a .NET Standard application using MSBuild, Windows Server, AWS Beanstalk, and GitHub Actions. With this pipeline in place, you can easily build, test, and deploy your application with confidence.

## 👉 **Checkout GitHub Repository for projects:**

**🔗** [**github.com/sumanprasad007**](http://github.com/sumanprasad007)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685557869584/83798879-b1f8-4857-b884-f8c2ef3213a2.png align="left")