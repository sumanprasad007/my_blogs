---
title: "How to Log in to Your VM and Automate VM Creation"
datePublished: Sat Mar 11 2023 05:49:47 GMT+0000 (Coordinated Universal Time)
cuid: clf3jrrad000v09mk3oj4cxvr
slug: how-to-log-in-to-your-vm-and-automate-vm-creation
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1678513690880/55cb329a-e788-4b86-8e87-274e56515544.png
tags: aws, python, developer, devops, beginners

---

# **📍 Introduction:**

Virtual Machines (VMs) are a fundamental component of modern-day computing. VMs provide a convenient way to test software applications, isolate operating systems, and provide a flexible and cost-effective solution for hosting applications. In this blog post, we'll explore how to login to your VM and different ways to automate the creation of VMs.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678513752151/289e2437-78e7-4579-a90c-f4d8c456ea39.png align="center")

# **📍 Ways to Connect to EC2 Instance**

How to Login to Our VM Connecting to your VM can be done in two ways - through a web browser or through SSH. Here are the steps for both methods:

## **🔹** Connect using Browser

1. Log in to the AWS Management Console.
    
2. Navigate to the EC2 dashboard.
    
3. Locate the instance that you want to connect to.
    
4. Click on the "Connect" button.
    
5. In the "Connect To Your Instance" window, select "EC2 Instance Connect" and click on "Connect".
    
6. A new browser window will open, and you will be automatically logged in to your instance.
    

Connect using SSH SSH (Secure Shell) is a widely used protocol for secure remote access. Here are the steps for connecting to your instance using SSH:

## **🔹** Putty & Putty Gen

1. Download and install Putty and PuttyGen.
    
2. Generate an SSH key pair using PuttyGen.
    
3. Copy the public key to your instance using the AWS Management Console.
    
4. Launch Putty and enter the public DNS of your instance.
    
5. In the "Connection" tab, expand the "SSH" tab and click on "Auth".
    
6. In the "Authentication Parameters" section, browse and select your private key file.
    
7. Click on "Open" to connect to your instance.
    

## **🔹** CMD for Windows, Terminal in Linux, or iTerm Terminal for MacBook

1. Open your terminal application.
    
2. Change the permissions of your key pair by typing "chmod 400 myKeyPair.pem" (replace "myKeyPair.pem" with your own key pair name).
    
3. Connect to your instance by typing "ssh -i /path/to/myKeyPair.pem ec2-user@PublicDNS" (replace "myKeyPair.pem" and "PublicDNS" with your own key pair name and the public DNS of your instance, respectively).
    

## **🔹** MobaXterm (Platform Independent)

1. Download and install MobaXterm.
    
2. Launch MobaXterm and click on the "Session" button.
    
3. Enter the public DNS of your instance and select "SSH" as the session type.
    
4. In the "Advanced SSH settings" section, click on the "Use private key" checkbox and browse and select your private key file.
    
5. Click on "OK" to connect to your instance.
    

# **📍 Ways to Automate VM Creation**

Different Ways to Automate the Creation of VM Automating the creation of VMs can save you time and effort, especially if you need to create many instances at once. Here are three ways to automate the creation of VMs:

## **🔹 AWS CLI**

Steps to Create EC2 Instance Using AWS CLI The AWS CLI (Command Line Interface) is a powerful tool that allows you to manage your AWS resources from the command line. Here are the steps to create an EC2 instance using AWS CLI:

1. Download and install the AWS CLI.
    
2. Authenticate and authorize using your AWS access and secret key by typing "aws configure".
    
3. Create an EC2 instance by typing "aws ec2 run -instances --image-id ami-xxxxxxxx --count 1 --instance-type t2.micro --key-name myKeyPair --security-group-ids sg-xxxxxxxx".
    
    Note: Replace "ami-xxxxxxxx", "myKeyPair", and "sg-xxxxxxxx" with your own AMI ID, key pair name, and security group ID, respectively.
    
    1. Wait for the instance to be created.
        
    2. Use the "aws ec2 describe-instances" command to verify that the instance has been created.
        
    
    ## **🔹 AWS CloudFormation Templates:**
    
    Steps to Create Using CloudFormation Templates CloudFormation is a service that allows you to define your AWS infrastructure as code. Here are the steps to create an EC2 instance using a CloudFormation template:
    
    1. Create a CloudFormation stack by navigating to the CloudFormation dashboard and clicking on "Create Stack".
        
    2. Select "Template is ready" and "Upload a template file".
        
    3. Choose a CloudFormation template from GitHub or upload one locally.
        
    4. Follow the instructions on the screen to create the stack.
        
    
    ## **🔹 AWS API - Python Boto3:**
    
    Steps to Create Using AWS API - Python Boto3 Boto3 is the AWS SDK for Python, which allows you to write Python scripts to automate AWS tasks. Here are the steps to create an EC2 instance using Boto3:
    
    1. Install Boto3 by typing "pip install boto3".
        
    2. Import the Boto3 library into your Python script.
        
    3. Authenticate and authorize using your AWS access and secret key.
        
    4. Create an EC2 instance by calling the "run\_instances" method of the EC2 client object.
        
    5. Wait for the instance to be created.
        
    6. Use the "describe\_instances" method to verify that the instance has been created.
        
    
    Beautiful Documentation of Boto3 Boto3 is a comprehensive Python library that allows you to interact with many AWS services. The Boto3 documentation is well-written and easy to navigate, with examples and code snippets for many AWS services. You can access the documentation at [**https://boto3.amazonaws.com/v1/documentation/api/latest/index.html**](https://boto3.amazonaws.com/v1/documentation/api/latest/index.html).
    

# **📍 Conclusion:**

In this blog, we discussed two important topics related to AWS: how to log in to your VM and how to automate the creation of VMs. We covered different methods to log in to your VM, such as connecting using a browser or SSH, and discussed different tools like Putty, MobaXterm, and NoMachine. We also explained the steps to automate the creation of VMs using AWS CLI, CloudFormation templates, and Python Boto3.

By mastering these skills, you can save time and effort and increase your productivity when working with AWS. Whether you are a developer, system administrator, or business owner, knowing how to log in to your VM and automate the creation of VMs can help you achieve your goals faster and more efficiently. So, start practising these techniques today and take your AWS skills to the next level!