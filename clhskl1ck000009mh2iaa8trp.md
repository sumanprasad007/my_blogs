---
title: "Aws Live Project | Deploy App Using Httpd"
datePublished: Thu May 18 2023 03:26:12 GMT+0000 (Coordinated Universal Time)
cuid: clhskl1ck000009mh2iaa8trp
slug: aws-live-project-deploy-app-using-httpd
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1684380580568/aa6a40c4-1804-4af4-babc-bb44bd3b66b6.jpeg
tags: software-development, aws, developer, devops, beginners

---

## **📍** Introduction:

In today's digital era, deploying applications on the cloud has become essential for businesses to leverage the scalability and flexibility offered by cloud platforms. Amazon Web Services (AWS) EC2 (Elastic Compute Cloud) is a popular choice for hosting applications due to its ease of use, reliability, and powerful features. In this blog, we will walk you through the step-by-step process of creating an IAM user, launching an EC2 instance, accessing it, deploying an application, exposing it to the outside world, and accessing the deployed application from your laptop. Let's dive in!

## **🔹** Creating an IAM User and Login:

IAM (Identity and Access Management) enables you to securely control access to AWS resources. Follow these steps to create an IAM user and log in:

Step 1: Open the AWS Management Console and navigate to the IAM service. \\

Step 2: Click on "Users" in the left navigation pane and then click on "Add User".

Step 3: Provide a user name and select the access type (Programmatic access, AWS Management Console access, or both).

Step 4: Set permissions for the user by adding them to one or more groups or attaching policies directly.

Step 5: Complete the user creation process and note down the access key ID and secret access key.

Code Snippet: Creating an IAM user programmatically using AWS CLI:

```plaintext
aws iam create-user --user-name <user-name>
```

## **🔹** Creating an EC2 Instance - Best Practices:

Launching an EC2 instance involves configuring various parameters such as instance type, security groups, key pairs, and more. Here are some best practices to follow:

a. Choose the appropriate EC2 instance type based on your application's requirements (e.g., t2.micro for low-traffic websites).

b. Use Amazon Machine Images (AMIs) that are regularly updated and maintained.

c. Configure security groups to allow only necessary inbound and outbound traffic.

d. Create and use key pairs for secure SSH access to your instances.

e. Leverage AWS CloudFormation or Infrastructure as Code (IaC) tools like AWS CDK or Terraform for repeatable and version-controlled infrastructure deployments.

## **🔹** Launching an EC2 instance using AWS Management Console:

1. Open the AWS Management Console and navigate to the EC2 service.
    
2. Click on "Launch Instance" and follow the wizard to configure instance details, security groups, storage, and more.
    
3. Select an AMI that suits your application requirements.
    
4. Configure networking options, such as VPC, subnets, and IP addressing.
    
5. Review and launch the instance.
    
6. Accessing the EC2 Instance: Once your EC2 instance is up and running, you need to access it to manage and deploy your applications. Follow these steps:
    

Step 1: Identify the public IP address or DNS name of your EC2 instance.

Step 2: Open a terminal or SSH client on your local machine.

Step 3: Use the SSH command to connect to your EC2 instance. Replace `key.pem` with your key pair file path and `public-ip` with your EC2 instance's public IP address or DNS name.

```plaintext
ssh -i <key.pem> ec2-user@<public-ip>
```

## **🔹** Deploying an Application on AWS EC2:

To deploy an application on your EC2 instance, you can choose from various methods such as manual deployment, using AWS Elastic Beanstalk, or using containerization with services like AWS ECS or EKS. Let's cover a simple manual deployment process:

Step 1: Connect to your EC2 instance using SSH (as explained in the previous step).

Step 2: Install the required dependencies, runtime, or framework for your application.

Step 3: Copy your application code or files to the EC2 instance using tools like SCP or Git.

Step 4: Configure your application by setting environment variables, updating configuration files, or installing additional libraries.

Step 5: Start your application by running the appropriate command or script.

## **🔹** Deploying a Node.js application on EC2:

1. Connect to your EC2 instance using SSH.
    
2. Install the Apache HTTP Server (HTTPD) on your EC2 instance using the following command:
    
    ```plaintext
    sudo yum install httpd -y
    ```
    
    Start the HTTPD service by running the following command:
    
    ```plaintext
    sudo service httpd start
    ```
    
    Verify that the HTTPD service is running by accessing the public IP address or public DNS name of your EC2 instance in a web browser. You should see the default Apache HTTP Server page.
    

## **🔹** Install Node.js and npm (Node Package Manager):

```plaintext
sudo yum install -y nodejs npm
```

1. Copy your application files to the EC2 instance using SCP or Git:
    

```plaintext
scp -i <key.pem> -r /path/to/your/app ec2-user@<public-ip>:~/app
```

1. Install application dependencies:
    

```plaintext
cd ~/app
npm install
```

1. Configure your application (e.g., update configuration files):
    

```plaintext
nano ~/app/config.js
```

1. Start your application:
    

```plaintext
node ~/app/index.js
```

## **🔹** Exposing the Application to the Outside World:

To make your application accessible from the internet, you need to configure inbound rules in your EC2 instance's security group to allow traffic on specific ports. Follow these steps:

Step 1: Open the AWS Management Console and navigate to the EC2 service.

Step 2: Select your EC2 instance and click on "Actions" &gt; "Networking" &gt; "Change Security Groups".

Step 3: Add a new security group or modify the existing security group associated with your EC2 instance.

Step 4: Configure inbound rules to allow traffic on the desired ports (e.g., HTTP on port 80, HTTPS on port 443).

Step 5: Save the changes.

## **🔹** Accessing the Application Deployed on AWS from Your Laptop:

To access the application deployed on AWS EC2 from your laptop, follow these steps:

Step 1: Open a web browser on your laptop.

Step 2: Enter the public IP address or DNS name of your EC2 instance in the browser's address bar.

Step 3: If you have exposed your application on port 80 (HTTP), you can directly access it using the IP address or DNS name. For example, `http://<public-ip>` or `http://<dns-name>`.

Step 4: If you have configured HTTPS (SSL/TLS) for your application, use `https://<public-ip>` or `https://<dns-name>`. Note that you may need to set up SSL certificates to enable HTTPS.

## **🔹** Configure DNS (Optional):

To access your application using a custom domain name instead of the EC2 instance's IP address or DNS name, you can configure DNS settings. Here's how:

a. Go to your preferred DNS provider (e.g., Route 53, GoDaddy, etc.).

b. Create a new DNS record (A record or CNAME record) and point it to the public IP address or DNS name of your EC2 instance.

c. Save the DNS record changes.

After the DNS records propagate, you can access your application using the custom domain name.

## **🔹** Set Up SSL/TLS Encryption (Optional):

To secure your application with SSL/TLS encryption, you can obtain an SSL certificate and configure it on your EC2 instance. Here's a high-level overview of the steps involved:

a. Obtain an SSL certificate from a trusted certificate authority (CA). You can use services like AWS Certificate Manager (ACM), Let's Encrypt, or purchase an SSL certificate from a CA. b. Install and configure the SSL certificate on your Apache HTTP Server running on the EC2 instance. c. Update the HTTPD configuration to enable HTTPS and redirect HTTP traffic to HTTPS.

The detailed steps for SSL/TLS certificate installation and configuration may vary depending on your specific setup and the SSL certificate provider. It's recommended to refer to the documentation provided by your certificate authority or follow the specific instructions provided by the SSL certificate provider.

## **🔹** Auto Scaling and Load Balancing (Optional):

To ensure high availability and handle varying traffic loads, you can leverage AWS Auto Scaling and Load Balancing services. These services automatically adjust the number of EC2 instances based on defined scaling policies and distribute traffic among multiple instances. Here's an overview of the process:

Step 1: Create an Auto Scaling group that defines the minimum and maximum number of instances.

Step 2: Configure scaling policies based on metrics like CPU utilization or request count.

Step 3: Create an Elastic Load Balancer (ELB) to distribute traffic across the instances in the Auto Scaling group.

Step 4: Configure the Auto Scaling group to use the ELB for load balancing.

Although Auto Scaling and Load Balancing add complexity, they provide benefits like fault tolerance, increased availability, and improved performance.

## **🔹** Continuous Integration and Deployment (Optional):

To streamline the application deployment process, you can incorporate continuous integration and deployment (CI/CD) pipelines. CI/CD pipelines automate the build, testing, and deployment of your application, ensuring a faster and more reliable deployment cycle. Here's a brief outline of the process:

Step 1: Set up a source code repository (e.g., Git) to store your application code.

Step 2: Configure a CI/CD tool (e.g., AWS CodePipeline, Jenkins) to monitor the repository for changes.

Step 3: Define build and test stages in your pipeline to compile the code, run tests, and generate artifacts.

Step 4: Add a deployment stage to the pipeline, which triggers the deployment of your application to the EC2 instance.

Step 5: Test the pipeline by making changes to your application code and observing the automated deployment process.

Implementing CI/CD pipelines can significantly enhance the efficiency and reliability of your deployment workflow.

## **📍**Conclusion:

In this comprehensive guide, we covered the essential steps for deploying applications on AWS EC2. We explored creating an IAM user, launching an EC2 instance following best practices, accessing the instance, deploying an application manually, exposing the application to the outside world, and accessing it from your laptop. By following these steps and understanding the provided code snippets, you can confidently deploy and manage your applications on AWS EC2, taking advantage of the scalability and reliability of the cloud. In this comprehensive guide, we covered additional advanced topics that can further enhance your application deployment on AWS EC2. We explored Auto Scaling and Load Balancing to improve scalability and availability, and we touched upon the importance of incorporating CI/CD pipelines to automate the deployment process.

Remember, AWS offers a wide range of services and deployment options, so feel free to explore and adapt these steps to your specific needs. Happy deploying!

## **🔹 Checkout GitHub Repository for projects:**

🔗 [**github.com/sumanprasad007**](http://github.com/sumanprasad007)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684256136175/44305bb4-89c4-49f0-98aa-b16c3db06727.png?auto=compress,format&format=webp align="left")