---
title: "Deploying and Exposing a NodeJS Application to the External World with AWS EC2"
datePublished: Sun Mar 19 2023 05:50:28 GMT+0000 (Coordinated Universal Time)
cuid: clfezbg10000d09lbgr50a6ic
slug: deploying-and-exposing-a-nodejs-application-to-the-external-world-with-aws-ec2
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1679204421589/fafe19cf-9470-4068-b7a8-0f9119ecd14c.webp
tags: aws, python, developer, devops, beginners

---

# **📍 Introduction:**

Hi Everyone, welcome to Day-12 of our learning series. In this session, we will cover how to deploy and expose a NodeJS application to the external world using AWS EC2. We will provide a live example and the source code is available on our GitHub repository.

## **🔹** Session Content:

1. Creating an IAM User and Login: The first step is to create an IAM (Identity and Access Management) user and login to AWS. IAM allows you to manage users and their access to AWS services.
    
2. Creating an EC2 Instance: We will then cover how to create an EC2 instance. EC2 is a virtual server in the cloud and it is essential to have good practices when creating instances. We will discuss some of these practices.
    
3. Accessing the EC2 Instance: Once the instance is created, we will learn how to access it through the command line interface or a web browser.
    
4. Deploying an Application on AWS EC2: Next, we will cover how to deploy a NodeJS application on AWS EC2. We will provide step-by-step instructions and discuss best practices.
    
5. Exposing the Application to the Outside World: After deploying the application, we will demonstrate how to expose it to the outside world. This will allow users to access the application from anywhere with an internet connection.
    
6. Accessing the Application Deployed on AWS from Your Laptop: Finally, we will show you how to access the application deployed on AWS from your laptop.
    

## **🔹**Summary:

In this session, we covered the process of deploying and exposing a NodeJS application to the external world using AWS EC2. We discussed the steps involved in creating an IAM user, creating an EC2 instance, accessing it, deploying an application, and exposing it to the outside world. We hope this session was helpful and informative for you. You can find the source code on our GitHub repository for further reference. Thank you for attending this session.

# **📍 Steps to follow along:**

# **🔹** Deploying a Node Js Application on AWS EC2

### ⚜Testing the project locally

1. Clone this project
    

```python
git clone https://github.com/verma-kunal/AWS-Session.git
```

1. Setup the following environment variables - `(.env)` file
    

```python
DOMAIN= ""
PORT=3000
STATIC_DIR="./client"

PUBLISHABLE_KEY=""
SECRET_KEY=""
```

1. Initialise and start the project
    

```python
npm install
npm run start
```

### ⚜ Set up an AWS EC2 instance

1. Create an IAM user & login to your AWS Console
    
    * Access Type - Password
        
    * Permissions - Admin
        
2. Create an EC2 instance
    
    * Select an OS image - Ubuntu
        
    * Create a new key pair & download `.pem` file
        
    * Instance type - t2.micro
        
3. Connecting to the instance using ssh
    

```python
ssh -i instance.pem ubunutu@<IP_ADDRESS>
```

### ⚜ Configuring Ubuntu on remote VM

1. Updating the outdated packages and dependencies
    

```python
sudo apt update
```

1. Install Git - [Guide by DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-install-git-on-ubuntu-22-04)
    
2. Configure Node.js and `npm` - [Guide by DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-ubuntu-22-04)
    

### ⚜ Deploying the project on AWS

1. Clone this project in the remote VM
    

```python
git clone https://github.com/verma-kunal/AWS-Session.git
```

1. Setup the following environment variables - `(.env)` file
    

```python
DOMAIN= ""
PORT=3000
STATIC_DIR="./client"

PUBLISHABLE_KEY=""
SECRET_KEY=""
```

> For this project, we'll have to set up an [Elastic IP Address](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/elastic-ip-addresses-eip.html) for our EC2 & that would be our `DOMAIN`

1. Initialise and start the project
    

```python
npm install
npm run start
```

> NOTE - We will have to edit the **inbound rules** in the security group of our EC2, in order to allow traffic from our particular port

# **📍 Resources:**

> * Video Link by Abhishek Veermalla Sir: [https://youtu.be/NLmF64KdLN0?list=PLdpzxOOAlwvIKMhk8WhzN1pYoJ1YU8Csa](https://youtu.be/NLmF64KdLN0?list=PLdpzxOOAlwvIKMhk8WhzN1pYoJ1YU8Csa)
>     
> * GitHub by Kunal Verma + Readme file: [https://github.com/verma-kunal/AWS-Session](https://github.com/verma-kunal/AWS-Session)
>     
> * Image Credit + Blog: [https://sumantmishra.medium.com/how-to-deploy-node-js-app-on-aws-with-github-db99758294f1](https://sumantmishra.medium.com/how-to-deploy-node-js-app-on-aws-with-github-db99758294f1)
>     
> 
> ### ⚜ Follow Prasad Suman Mohan for many such contents:
> 
> * LinkedIn: [https://www.linkedin.com/in/prasad-suman-mohan/](https://www.linkedin.com/in/prasad-suman-mohan/)
>     
> * Blog: [https://sumanprasad.hashnode.dev/](https://sumanprasad.hashnode.dev/)
>