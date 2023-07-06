---
title: "End to End CI/CD pipeline using AWS Cloud for my Portfolio Website🔥"
datePublished: Thu Jul 06 2023 04:13:53 GMT+0000 (Coordinated Universal Time)
cuid: cljqmv38h000e09mffwl8aef7
slug: end-to-end-cicd-pipeline-using-aws-cloud-for-my-portfolio-website
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1688388608385/68a4232b-d2c2-4132-8e04-cfb0c8c64324.png
tags: software-development, aws, developer, devops, beginners

---

# **📍 Introduction**

The concept of Continuous Integration (CI) and Continuous Deployment (CD) has become increasingly popular in the software development industry, as organizations strive to streamline their software delivery processes and reduce errors. CI/CD are practices that aim to automate the process of building, testing, and deploying software, enabling developers to deliver new features and bug fixes to production faster and with greater confidence. Implementing CI/CD pipelines has been made easier by the usage of cloud computing platforms like Amazon Web Services (AWS).

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688387115827/df5ca882-d4c8-4fe7-befb-8fd17607c3d3.png align="center")

## **✔** Features of Project:

**1.     Comprehensive Study:** The Report provides a comprehensive analysis of the steps involved in implementing a complete CI/CD pipeline using AWS. The study covers all the key components of a CI/CD pipeline and explains how they can be automated using various AWS services. This allows organizations to understand the end-to-end process of creating a CI/CD pipeline, from code management to deployment.

**2.     The Benefits of using AWS:** The Report highlights the key benefits of using AWS to create a CI/CD pipeline. These benefits include increased speed, as automation reduces the time taken for manual processes, reduced errors, as automation eliminates human error, improved collaboration, as developers can work together on the same source code,

**3.     scalability:** Organizations can scale their infrastructure as required, and enhanced security, as AWS implements various security measures to ensure the safety of customer data.

**4.     Case Study:** The Report includes a case study that demonstrates how a complete CI/CD pipeline can be created using AWS. This provides organizations with a practical example of how the different components of a CI/CD pipeline can be automated using AWS services. The case study also provides recommendations for organizations looking to adopt a similar approach, allowing them to learn from the experience of others.

**5.     AWS Services:** The Report explores the various AWS services that can be used to automate the different stages of a CI/CD pipeline, such as GitHub for code management, AWS CodeBuild for building and testing code, and AWS CodeDeploy for deployment. The Report explains how each of these services can be used and how they integrate to create a complete CI/CD pipeline.

**6.     Recommendations:** The Report ends with a list of suggestions for businesses wishing to use Amazon to construct a full CI/CD pipeline. These suggestions include advice on best practices, such as how to choose the proper Amazon services, how to assure security, and how to grow the infrastructure to meet the requirements of the software delivery process.

**7.     Security:** The Report also addresses the security aspect of using AWS for a CI/CD pipeline, highlighting the various measures implemented by AWS to ensure the safety of customer data. These measures include network security, data encryption, and access control.

**8.     Scalability:** While discussing the scalability of utilising Amazon for a CI/CD pipeline, the Report emphasises how simple it is for businesses to extend their infrastructure to match the needs of their software delivery process. With AWS services, businesses can scale their infrastructure up or down as needed without having to make substantial initial hardware expenditures.

## **✔ Tools involve in the project:**

1. **AWS CodeBuild:** This completely managed-to-build service compiles source code, performs tests, and generates software packages that are prepared for deployment. You won't need to set up, maintain, or grow your build servers anymore, freeing you your time to focus on creating code rather than taking care of infrastructure.
    
2. **AWS CodeDeploy:** It is a fully-managed deployment service that automates software deployments to a variety of computing services, including Amazon EC2 instances, AWS Lambda functions, and on-premises servers. It eliminates the need for you to manually deploy your application code and ensures that your deployments are consistent, error-free, and repeatable.
    
3. **AWS CodePipeline:** It is a fully managed continuous delivery service that helps you automate your release pipelines for fast and reliable application and infrastructure updates. It orchestrates and automates the different stages of your release process, including building, testing, and deploying your code changes.
    
4. **AWS S3:** It is a cloud-based object storage service offered by Amazon Web Services (AWS). It provides scalable and secure storage for a wide range of use cases, such as data backup, content distribution, and application data storage. In the context of a CI/CD pipeline, S3 is often used for storing artifacts and deploying applications
    
5. **AWS EC2**: It is a web service that provides resizable computing capacity in the cloud. For developers, it is intended to make web-scale cloud computing simpler. To meet the unique requirements of the project, EC2 instances can be deployed with a number of operating systems and programmes.
    
6. **AWS IAM:** It is a web service that helps you securely control access to AWS resources for your users. IAM allows you to create and manage AWS users and groups, and control their access to AWS services and resources using permissions. You can use IAM to manage who can sign in to your AWS account, create and manage AWS users, groups, and roles, and assign granular permissions to users and groups to access specific resources.
    
7. **AWS VPC:** It is a service that lets you launch AWS resources into a virtual network that you define. This virtual network is logically isolated from other virtual networks in the AWS cloud, giving you complete control over your virtual networking environment. With VPC, you can create a virtual network topology that closely resembles a traditional network that you might operate in your own data centre, with multiple subnets, routing tables, and access control policies.
    
8. **AWS CloudWatch:** It is a monitoring and management service provided by Amazon Web Services (AWS) for applications, infrastructure, and services running on the cloud. CloudWatch collects and tracks metrics, collects and monitors log files, and sets alarms. It allows users to gain system-wide visibility into resource utilization, application performance, and operational health.
    
9. **GitHub:** It is a popular web-based platform that allows developers to collaborate on and manage software projects using the Git version control system. It provides a range of features for source code management, including version control, issue tracking, project management, code review, and collaboration tools.
    

# **📍 Project Creation step by step:**

### **✔ Step 1: Creating Pre-requisites:**

IAM Role Creations:

i. A role for CodeBuild: AWSCodePipelineServiceRole-us-east-1-website\_pipeline

**Policy Names:**

* AmazonS3FullAccess
    
* CloudWatchFullAccess
    
* AWSCodeBuildAdminAccess
    

ii. A role for CodeDeploy: devopsCodeDeployRole \[5\]

**Policy Names:**

* AmazonS3FullAccess
    

iii. A Role for EC2 Instance: CodeDeploy-Role-for-EC2 \[7\]

**Policy Names:**

* AmazonEC2FullAccess
    
* AmazonEC2RoleforAWSCodeDeploy
    
* AmazonS3FullAccess
    
* AWSCodeDeployFullAccess
    
* AWSCodeDeployRole
    
* AmazonEC2RoleforAWSCodeDeployLimitation
    

### **✔ Step 2: Now, it’s time to create An EC2 Instance & configure it:**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688388757566/37acc60c-4925-40ae-8c4e-c23c932310e7.png align="center")

i. Installing CodeDeploy on EC2

Steps to follow along:

1. Connect to the Instance using:
    
    * Putty & Putty-gen Software
        
    * Command Prompt or PowerShell by following the below:
        
    * Connect to the SSH client and copy the Example text.
        

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688388819295/084122db-4d9b-4640-bec9-427a7d714463.png align="center")

1. Open the File Manager and locate the folder where you have downloaded your Key-pair. In the search bar, type `cmd` and hit the Enter button. Now, paste the Example text to connect with the EC2 instance.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688388866556/12fe2198-2710-498b-bdcb-f27c4c4cf26a.png align="center")
    
2. We have successfully logged in to our console.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688388892123/d530ffd1-d2a4-499b-957b-e5fe9e206793.png align="center")

1. Now first, update the instance, and then we will create a shell script to install the CodeDeploy agent. It's even possible by entering single commands one by one, but it's always a good practice to execute using the shell script.
    
2. Save and exit from the vi (editor) by pressing `esc`, `:`, `wq!`.
    
3. Now, we will execute the shell script to install the CodeDeploy Agent.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688388928475/0b2550fb-52d0-4ce8-b11e-8c00aedbfd68.png align="center")

* Run ./[install.sh](http://install.sh) command and press enter
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688388951920/6b4b0833-98f0-48ac-9862-de2028b45d3a.png align="center")

* Validate CodeDeploy agent is running or not using the following command:
    
* **sudo service codedeploy-agent status**
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688388978254/7b6425d8-729d-40ba-add6-e45ff5bf7b46.png align="center")

### **✔** Step 3: Creating the Build Stage

a. Source Stage Configuration:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688392498369/47d90264-bad4-4589-b268-392fde4b2afd.png align="center")

b. Build Stage Configuration:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688392517482/33d55f35-2937-487f-b9a9-2e1ebcd8797c.png align="center")

c. Deploy Stage Configuration:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688392532968/1591f290-3bb9-4466-a1e1-99ad562f5b0e.png align="center")

d. Reviewing the Pipeline:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688392745379/12313733-4888-4504-a80a-0eed2813152d.png align="center")

e. Created Pipeline with all the stages defined:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688392768013/50c47785-a569-4738-b54d-7c17b683ef06.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688392773188/f7f2c641-5fb6-45a6-a182-4d69664ecf9c.png align="center")

f. Encountered Unknown error due to lack of CodeDeploy agent on EC2 Server:

This problem was caused by us failure to install the Code Deploy agent on our EC2 server:

Let us Install and Configure CodeDeploy Agent:

g. Below are commands to install it:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688392791174/37247b03-8ea1-4d51-bdd9-3eb2e02c17f5.png align="center")

### **✔** Step 6: Source Code Modification to Re-run the Pipeline:

a. Source Code After Modification:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688392808309/91b01115-f697-47e3-80d2-aa13b279308b.png align="center")

b. Committed & pushed the changes to the repository:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688392822225/5afe5818-e6d5-49c6-b5af-52f3da779f1d.png align="center")

c. Our website is live and running using the Public Ip of our EC2 Instance:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688392835795/df6a212f-9618-4078-9232-035623d1ccbc.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688392840265/f3481541-e305-4479-908f-bac4f4de45f0.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688392846274/37e0b3ef-38f2-4e47-8c13-6e33a192e131.png align="center")

d. Server Monitoring:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688392870210/b208caf1-ad47-4355-befb-a13ef9ccbade.png align="center")

# **📍 Results and Discussion**

With the proposed solution, the development team can easily track changes in the code repository and collaborate on the same source code. This has resulted in faster development and delivery of new features and bug fixes to production, reducing the time to market. Automated testing using AWS CodeBuild has significantly reduced the occurrence of errors, as it eliminates human error in the testing process. This has led to increased confidence in the software delivery process and improved customer satisfaction. The scalability of the proposed solution has been a significant advantage, as organizations can easily scale their infrastructure as required without having to make substantial initial hardware expenditures. This has allowed small startups to compete with large enterprises, providing a level playing field in the software development industry. The security measures implemented by AWS have ensured the safety of customer data, protecting it from unauthorized access and cyber-attacks. This has increased customer trust and confidence in the software delivery process. Overall, the proposed solution of implementing a CI/CD pipeline using AWS services has shown significant improvements in the software delivery process, reducing errors, increasing speed, and improving collaboration, scalability, and security.

### **✔ Applications:**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688388415767/fba6dbc8-56ec-421b-a7c1-b55b91dc1dfb.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688388431319/6c152d90-39bc-4361-a9eb-4450861c41c2.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688388452007/2cfa1ac1-9e6e-4167-b090-01351368d42b.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688388467325/38e54f57-5910-4fd5-8581-ace838b22ca7.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688388483069/2ff2e685-3cc5-4df7-8f24-65907430f530.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688388498267/d6f9c098-7663-4541-b9e1-d56875e74a91.png align="center")

# **📍 CONCLUSION**

In conclusion, implementing a complete CI/CD pipeline using AWS can provide significant benefits to organizations looking to streamline their software delivery processes. By automating the different stages of the pipeline using services such as GitHub, AWS CodeBuild, and AWS CodeDeploy, organizations can speed up cooperation, decrease the likelihood of errors, and cut down on the time and effort needed to deploy software.

The proposed solution for the implementation of the CI/CD pipeline using AWS is a comprehensive approach that includes several stages, from source code management to testing and deployment. The architecture of the proposed solution includes various AWS services, such as GitHub, CodeBuild, CodeDeploy, and CloudFormation, which are combined to create a complete CI/CD pipeline.

### **🔍 Checkout GitHub Repository for projects:**

**🔗** [https://github.com/sumanprasad007/BTech\_CTIS-\_Complete-CI-CD-pipeline-using-AWS-for-an-Application\_2019-B-15112001A.git](https://github.com/sumanprasad007/BTech_CTIS-_Complete-CI-CD-pipeline-using-AWS-for-an-Application_2019-B-15112001A.git)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688616690432/b4b68267-a8f7-45b6-a068-042a27a74a8e.png align="center")