---
title: "PROJECT - Deploying a React-Django Application on AWS ECS 🌐"
datePublished: Sat Aug 26 2023 03:49:21 GMT+0000 (Coordinated Universal Time)
cuid: cllrhfzfz000109lcbyg4f12p
slug: project-deploying-a-react-django-application-on-aws-ecs
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1692965995259/e992b39e-87aa-498c-abaf-f13d63c12bd1.png
tags: aws, developer, devops, containers, 90daysofdevops

---

# **Introduction:**

Containerization and cloud-based deployment are at the forefront of modern application development. In this comprehensive guide, we'll walk you through deploying a React application using an AWS ECS (Elastic Container Service) cluster container. This approach offers scalability, manageability, and reliability for your React app. Let's dive in! 🌐

## **Key Features of This Project 🌟**

This project boasts several exciting features that make it a powerful choice for deploying your React applications:

* **Simplified Deployment**: Containerization simplifies deployment, ensuring your app runs consistently across various environments.
    
* **Scalability**: AWS ECS allows you to scale your application effortlessly as your user base grows.
    
* **Isolation**: Containers provide isolation, preventing conflicts between your app and the underlying system.
    
* **Resource Efficiency**: Containers use resources efficiently, enabling you to maximize the utilization of your infrastructure.
    
* **Version Control**: Docker images and ECS task definitions offer version control for your app, making it easy to roll back if issues arise.
    
* **Security**: AWS ECS provides robust security features to protect your application and data.
    
* **High Availability**: ECS ensures high availability by distributing tasks across multiple instances.
    
* **Monitoring and Logging**: AWS offers comprehensive monitoring and logging capabilities to keep an eye on your app's performance.
    
* **Cost Optimization**: With AWS, you can optimize costs by scaling resources according to demand.
    

Now, let's embark on the journey of deploying your React app using AWS ECS. 🚢

## **Prerequisites 🛠️**

Before we dive into the deployment process, make sure you have the following prerequisites in place:

* **Clone the Repository**: Start by cloning the application repository from GitHub. Locally and will use this code to send it to our ECR for our ease and You can do this using the following command:
    
    ```plaintext
    git clone https://github.com/chxtan/react_django_demo_app
    ```
    
* **Install Docker and AWS CLI**:
    
    Docker is essential for containerization, and the AWS CLI allows us to interact with AWS services from the command line. You can download Docker [**here**](https://www.docker.com/get-started) and the AWS CLI [**here**](https://aws.amazon.com/cli/).
    
* **Configure AWS**:
    
    Run the `aws configure` command and enter your AWS access key, secret key, region, and output format when prompted. These credentials should belong to a user with the necessary permissions for the AWS services we'll be using.
    
* **Create a User with Programmatic Access**:
    
    To create a user with programmatic access, head to the AWS Identity and Access Management (IAM) console and follow the instructions to create a user and generate access keys.
    
* ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692965067340/320218a4-b20f-4ff9-8d9d-943d1634ef99.png align="center")
    

🔧 **Setting Up the Elastic Container Registry (ECR)**

* **Navigate to ECR**: In the AWS console, go to the Elastic Container Registry (ECR) service.
    
* **Create a Public Repository**: Click on "Create repository" and provide the required details for your repository. This is where your Docker images will be stored.
    
* **Repository Created**: Once created successfully, you'll see a confirmation message like the one below:
    

🐳 **Building and Pushing Docker Images**

* **Push Docker Images**: In your project directory, you'll find a set of commands provided under "View Push Command." Execute these commands on your EC2 instance. This will build and push your Docker images to the ECR repository.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692965088587/a3d2f757-ec70-49f7-a880-8a8113ad5979.png align="center")
    
* After executing these commands, your Docker images will be pushed to the repository.
    
* ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692965124772/df505ef0-3341-4a31-93b6-12310036a481.png align="center")
    

⚙️ **Configuring Amazon ECS**

* **Create an ECS Cluster**: Now, navigate to Amazon Elastic Container Service (ECS) in the AWS console and create an ECS cluster. This cluster will manage your containerized application.
    
* ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692965141837/e6509db4-7fb4-4a5e-b28c-787b245a6bc3.png align="center")
    
* **Task Definitions**: On the left-hand side, select "Task Definitions."
    
* **Configure Task Definition**: Create a new task definition by specifying the task name, container name, and the URL of the Docker image from your ECR repository. Click "Create."
    
* ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692965158392/68f8554b-3b16-4233-9762-61c2edc1fef7.png align="center")
    
* **Active Task**: You'll notice that the task status is now active, indicating that the task definition is configured correctly.
    

🏃‍♀️ **Running the Task**

* **Run Task**: Select the task and click on "Run Task."
    
* **Configure Cluster and Security Group**: Choose the existing cluster (ecr\_ecs) and create a new security group that allows traffic on port 8000.
    
* ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692965212820/a57a1140-ccf6-436f-a0a4-affb06c53207.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692965225448/fb099315-f0ec-486d-a44f-4c0a608def25.png align="center")
    
    **Start the Task**: Save the configuration, and the task inside the container's task definition will start running.
    

🌐 **Accessing Your Application**

* **Get Public IP**: Once the task is running, copy the public IP of the container, appending port 8000 to it. Your site will now be live and accessible via this URL.
    

Congratulations! You've successfully deployed a React-Django application on AWS using Docker containers and Amazon ECS. This setup allows for scalability and efficient management of your application in a production environment. 🎉

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692691910505/ce439133-0dae-459a-8f82-000d91729fbb.png align="center")

### **🔍 Checkout GitHub Repository for projects:**

**🔗** [**github.com/sumanprasad007**](http://github.com/sumanprasad007)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692607442282/98c6c100-886d-4894-80bc-db5df0141100.png?auto=compress,format&format=webp align="left")

### **🔍 Check out my YouTube channel - Prasad Suman Mohan:**

🔗 [**youtube.com/@sumanprasad007**](http://youtube.com/@sumanprasad007)

%[https://youtu.be/oVJoN5Zc3Kw]