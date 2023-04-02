---
title: "Jenkins Zero to Hero: How to Install, Configure and Use Jenkins for CI/CD on AWS EC2 Instance"
datePublished: Sun Apr 02 2023 06:31:46 GMT+0000 (Coordinated Universal Time)
cuid: clfz0yhza00000amb3rl27vq9
slug: jenkins-zero-to-hero-how-to-install-configure-and-use-jenkins-for-cicd-on-aws-ec2-instance
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1680417073007/3d6b0102-2036-410a-ae4d-67d48bf0643b.png
tags: linux, python, developer, devops, beginners

---

# **📍 Introduction:**

Jenkins is an open-source automation server that enables developers to automate their software development process by building, testing, and deploying their code. In this tutorial, we will learn how to install, configure and use Jenkins for CI/CD on an AWS EC2 instance.

Prerequisites Before we proceed, make sure that you have an AWS account and an EC2 instance running with the Ubuntu operating system. Also, ensure that you have Java Development Kit (JDK) installed on your instance. You can use the following command to install JDK.

# **📍 Install Java JDK:**

```python
sudo apt update
sudo apt install openjdk-11-jre
```

Install Jenkins Once you have JDK installed on your EC2 instance, you can proceed with the installation of Jenkins. Follow the below steps to install Jenkins.

## **🔹** Step 1: Add Jenkins repository key to the system

```python
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
```

## **🔹** Step 2: Add the Jenkins repository to your system

```python
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
```

## **🔹** Step 3: Update your system and install Jenkins

```python
sudo apt-get update
sudo apt-get install jenkins
```

## **🔹** Step 4: Open port 8080 in the inbound traffic rules of your EC2 instance

By default, Jenkins will not be accessible to the external world due to the inbound traffic restriction by AWS. Open port 8080 in the inbound traffic rules as shown below.

1. Go to your AWS EC2 console
    
2. Click on Instances and select your running instance
    
3. In the bottom tabs, click on Security groups
    
4. Add inbound traffic rules as shown in the image (you can just allow TCP 8080 as well, in my case, I allowed All traffic).
    

## **🔹** Step 5: Login to Jenkins using the below URL:

```python
http://<ec2-instance-public-ip>:8080
```

Note: If you are not interested in allowing All Traffic to your EC2 instance, you can delete the inbound traffic rule for your instance or edit the inbound traffic rule to only allow custom TCP port 8080.

## **🔹** Step 6: Retrieve the Jenkins Admin Password

Run the command to copy the Jenkins Admin Password

```python
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

## **🔹** Step 7: Install suggested plugins

Click on Install suggested plugins and wait for Jenkins to Install suggested plugins.

## **🔹** Step 8: Create First Admin User (Optional)

You can create a first admin user or skip this step if you want to use this Jenkins instance for future use cases as well.

# **📍 Install Docker Pipeline Plugin:**

Install the Docker Pipeline plugin in Jenkins Now that we have installed and configured Jenkins, we can proceed with the installation of the Docker Pipeline plugin in Jenkins. Follow the below steps to install the Docker Pipeline plugin.

Step 1: Log in to Jenkins.

Step 2: Go to Manage Jenkins &gt; Manage Plugins.

Step 3: In the Available tab, search for "Docker Pipeline".

Step 4: Select the plugin and click the Install button.

Step 5: Restart Jenkins after the plugin is installed.

Docker Slave Configuration After the installation of the Docker Pipeline plugin, we need to configure Docker as the agent. Follow the below steps to configure Docker as the agent.

# **📍 Install Docker on EC2:**

## **🔹** Step 1: Install Docker on the EC2 instance

Docker is a containerization platform that allows you to package an application with all of its dependencies into a container. This container can then be run on any system that supports Docker, making it an excellent tool for building and deploying applications. To install Docker on the EC2 instance, follow the steps below.

1. SSH into the EC2 instance:
    

To install Docker, you need to SSH into the EC2 instance using an SSH client like PuTTY or the built-in terminal on a Unix-based system. If you are using PuTTY, enter the EC2 instance's public IP address or DNS name in the "Host Name" field, and then click "Open."

1. Update the package index:
    

Before installing any new packages, it is a good practice to update the package index on the EC2 instance.

```python
sudo apt-get update
```

1. Install Docker:
    

Once the package index is updated, you can install Docker by running the following command:

```python
sudo apt-get install docker.io
```

This command will download and install the Docker package along with its dependencies.

1. Grant Jenkins and Ubuntu user permissions to Docker daemon:
    

By default, the Docker daemon can only be run by the root user. However, we want to allow the Jenkins and Ubuntu users to run Docker commands without having to use sudo every time. To do this, we need to add the Jenkins and Ubuntu users to the Docker group.

```python
sudo usermod -aG docker jenkins
sudo usermod -aG docker ubuntu
```

1. Restart the Docker daemon:
    

Finally, restart the Docker daemon to apply the new group membership.

```python
sudo systemctl restart docker
```

Now that Docker is installed and the Jenkins user has been granted permissions to the Docker daemon, we can proceed to the next step of configuring Jenkins as a Docker agent.

## **🔹** Step 2: Configure Docker as a Jenkins agent

In this step, we will configure Docker as an agent in Jenkins. This means that Jenkins will use Docker containers to run build and test jobs, rather than running them directly on the EC2 instance.

1. Install the Docker Pipeline plugin in Jenkins:
    

Log in to Jenkins and navigate to "Manage Jenkins" &gt; "Manage Plugins." In the "Available" tab, search for "Docker Pipeline" and select the plugin. Click the "Install without restart" button.

1. Restart Jenkins:
    

Once the plugin is installed, Jenkins will prompt you to restart the server to apply the changes. Click the "Restart Jenkins when installation is complete and no jobs are running" checkbox and then click "Continue."

1. Configure the Docker agent in Jenkins:
    

Navigate to "Manage Jenkins" &gt; "Configure System" and scroll down to the "Cloud" section. Click the "Add a new cloud" dropdown and select "Docker." In the "Docker" section, enter a name for the Docker agent, select "Connect with Docker API" as the "Docker Host URI," and enter "tcp://[localhost:2375](http://localhost:2375)" as the value.

1. Configure the Docker image to use:
    

Scroll down to the "Docker Agent templates" section and click "Add Docker Template." Enter a name for the template, such as "Ubuntu Docker Image," and select the "Docker image" option. Enter the name of the Docker image to use, such as "ubuntu:latest," in the "Docker image" field.

1. Configure the Docker Container Startup Options
    

To configure the Docker container startup options, we need to create a Jenkins agent container that will run on the EC2 instance.

We will use the Docker Pipeline plugin to create the agent container. This plugin allows us to create a Docker container as a build agent dynamically.

To create the agent container, follow these steps:

1. In Jenkins, click on "New Item" to create a new job.
    
2. Enter a name for the job and select "Pipeline" as the job type.
    
3. Click "OK" to create the job.
    
4. In the Pipeline script section, enter the following script:
    

```python
pipeline {
  agent {
    docker { image 'node:16-alpine' }
  }
  stages {
    stage('Test') {
      steps {
        sh 'node --version'
      }
    }
  }
}
```

This script defines a pipeline with one stage that will run on an Ubuntu Docker container. The container will mount the Docker socket to allow the pipeline to run Docker commands on the host.

1. Click "Save" to save the job.
    

Now that the job is created, we can run it to test the Docker container startup options.

1. Click on "Build Now" to run the job.
    
2. Wait for the job to complete.
    

The job will create a Docker container with the specified options and run a "Node --version" command on it. If everything is configured correctly, you should see the output "Node Version" in the job console output.

Congratulations! You have successfully configured the Docker container startup options in Jenkins.

# **📍 Conclusion:**

Jenkins is a popular automation tool that can be used to automate building, testing, and deploying software applications. In this tutorial, we will walk you through the process of setting up Jenkins on an AWS EC2 instance, configuring Docker as an agent, and setting up a CI/CD pipeline for deploying applications to Kubernetes. We will cover everything from installing Java and Jenkins to configuring Docker, setting up a Jenkins slave node, and installing the Docker Pipeline plugin.

## **🔹** Step-by-Step Guide:

1. Launch an EC2 instance on the AWS console and install Java and Jenkins
    
2. Open port 8080 in the inbound traffic rules to access Jenkins
    
3. Install the Docker Pipeline plugin in Jenkins
    
4. Install Docker on the EC2 instance
    
5. Configure the Docker container startup options
    
6. Grant Jenkins user and Ubuntu user permission to the Docker daemon
    
7. Restart Jenkins to apply changes
    
8. Configure Docker as a Jenkins slave node