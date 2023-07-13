---
title: "📝 Configuring Jenkins Declarative Pipeline with AWS Cloud 🚀"
datePublished: Thu Jul 13 2023 04:20:21 GMT+0000 (Coordinated Universal Time)
cuid: clk0n6dcr000709ladtb19qnb
slug: configuring-jenkins-declarative-pipeline-with-aws-cloud
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1689188419507/ddb989e8-68ba-4108-b7c4-97fac3456c0a.png
tags: software-development, aws, developer, devops, beginners

---

# **📍 Introduction:**

Are you looking to configure Jenkins's declarative pipeline using AWS Cloud? 🤔 Look no further! In this blog, I will guide you through the step-by-step process with detailed instructions and commands. Let's get started! ⚙️

### 🔹 Step 1: Start an EC2 Server with Enabled Ports

To begin, launch an EC2 server and make sure to enable inbound rules for ports 22, 8080, and 8000. These ports are crucial for successful configuration.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689188986466/7eaad889-582d-4075-85b3-0cf6ca828a07.png align="center")

### 🔹 Step 2: Connect to the Server via SSH

Next, establish a connection to the server using the SSH command. This will allow you to interact with the server's command line.

### 🔹 Step 3: Update the Server

Once connected, update the server by running the following commands:

```plaintext
sudo apt update
git clone https://github.com/sumanprasad007/django-notes-app-with-database.git
cd django-notes-app-with-database
sudo apt install git docker.io -y
sudo usermod -aG docker ubuntu
sudo reboot
```

After the server reboots, reconnect using SSH.

Verify that Ubuntu has permission to run Docker by executing `docker images` command.

### 🔹 Dockerfile

Create a Dockerfile with the following content:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689189023579/41b986a4-0248-4ae5-a0c7-97e002fc0b57.png align="center")

```plaintext
FROM python:3.9
WORKDIR /app/backend
COPY requirements.txt /app/backend
RUN pip install -r requirements.txt
COPY . /app/backend
EXPOSE 8000
CMD python /app/backend/manage.py runserver 0.0.0.0:8000
```

Build the Docker image by running:

```plaintext
docker build -t my-note-app .
docker images
```

### 🔹 Step 4: Install Java JDK and Jenkins Using Shell Script

To install Java JDK and Jenkins, follow these steps:

1. Make the Jenkins installation script executable:
    

```plaintext
chmod +x jenkins-installation.sh
```

1. Run the Jenkins installation script:
    

```plaintext
./jenkins-installation.sh
```

Verify the Jenkins installation by checking its version:

```plaintext
jenkins --version
```

Grant Jenkins access to build and run Docker images:

```plaintext
sudo usermod -aG docker jenkins
sudo reboot
```

Access Jenkins by entering your EC2 instance's public IP followed by port 8080 in your browser. Obtain the initialAdminPassword by running:

```plaintext
cat /var/lib/jenkins/secrets/initialAdminPassword
```

Copy and paste the password in the provided tab and install all the necessary plugins.

### 🔹 Step 5: Creating a Declarative Pipeline

Now, let's create a declarative pipeline in Jenkins:

1. Click on "New Item" and name it "my-note-app-cicd-pipeline".
    
2. Under the configuration settings, select the GitHub project and provide the repository URL:
    

```plaintext
https://github.com/sumanprasad007/django-notes-app-with-database.git
```

Set the name to "note-app".

1. Enable the "Build Triggers" option by ticking the box next to "GitHub hook trigger for GITScm pooling".
    
2. In the "Pipeline" section, choose "Pipeline Script" and add the following script:
    

```plaintext
pipeline {
    agent any 
    
    stages{
        stage("Clone Code"){
            steps {
                echo "Cloning the code"
                git url:"https://github.com/sumanprasad007/django-notes-app-with-database.git", branch: "main"
            }
        }
        stage("Build"){
            steps {
                echo "Building the image"
                sh "docker build -t my-note-app ."
            }
        }
        stage("Push to Docker Hub"){
            steps {
                echo "Pushing the image to Docker Hub"
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                sh "docker tag my-note-app ${env.dockerHubUser}/my-note-app:latest"
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker push ${env.dockerHubUser}/my-note-app:latest"
                }
            }
        }
        stage("Deploy"){
            steps {
                echo "Deploying the container"
                sh "docker-compose down && docker-compose up -d"
                
            }
        }
    }
}
```

### ✔ Before building, make sure to follow these additional steps:

1. Add DockerHub credentials in the global credentials section with the ID as "dockerHub" along with the username and password.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689188784801/84584cba-e3e5-4817-be10-76d2eda76f9b.png align="center")
    
2. Create a Docker Compose file to enhance the deployment of Docker containers:
    

```plaintext
version: "3.3"
services:
  web:
    image: sumanprasad007/my-note-app:latest
    ports:
      - "8000:8000"
```

1. Install Docker Compose before running the pipeline.
    

Once everything is set up, you can manually trigger the pipeline by clicking the build button in the Jenkins interface.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689188811605/27fb4b13-b7a9-4e49-b5e8-81f27bddba31.png align="center")

### 🔹 Tadada: Our Note App is Successfully Deployed! 🎉

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689188826252/472d7ec2-5a6a-4289-8dcf-1026494b34b6.png align="center")

Congratulations! Your Note App is now deployed and ready to use. Enjoy the benefits of automation and continuous integration.

### 🔹 Bonus Step: Full Automation with Webhooks

To achieve full automation, configure webhooks so that any changes pushed to the GitHub repository will trigger the Jenkins pipeline and initiate the deployment process automatically.

🔹 Further Simplification with "Pipeline Script from SCM"

To make your pipeline more effective and easier to modify, you can use "Pipeline Script from SCM." This approach allows you to provide a GitHub repository link containing the Jenkinsfile. By adopting this method, any developer in your team with proper permissions can review and modify the Jenkinsfile, simplifying the pipeline management process.

### 📄 Jenkinsfile:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689188869732/7b8dc442-7c67-46f7-a84e-0c803d492a0a.png align="center")

```plaintext
Auto-trigger Jenkins pipeline using webhook

New commit: changed the title "Hello TWS Community Builders"
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689188923642/f1f0c96f-47ea-4bf5-b8a8-787375f346a8.png align="center")

By leveraging webhooks and the "Pipeline Script from SCM" approach, your team can work collaboratively on the Jenkinsfile and make changes with ease, eliminating the need to access the Jenkins dashboard.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689188844194/89875d01-efbb-45e8-bc92-ea040bea92c1.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689188851739/0f132f79-c08d-4ea6-8cd6-c4ca19fa6f0e.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689188899306/1c24a586-b1d3-46ba-bbb2-6dec150af89f.png align="center")

That's it! You have now successfully configured a Jenkins declarative pipeline using AWS Cloud. 🚀 Embrace automation and streamline your development workflow with this powerful setup. Happy coding! 👩‍💻👨‍💻

# 🔒 Conclusion 🔑

In this blog, we explored the step-by-step process of configuring a Jenkins declarative pipeline using AWS Cloud. By following the outlined instructions, you can automate your development workflow, enhance collaboration, and achieve continuous integration. Let's summarize the key points covered:

1️⃣ We started by setting up an EC2 server with the necessary ports enabled, allowing us to establish a secure connection.

2️⃣ After connecting to the server via SSH, we updated the server, installed Git, and Docker, and cloned the project repository.

3️⃣ Dockerfile was created to define the Docker image configuration, and we built the image using the Docker build command.

4️⃣ Java JDK and Jenkins were installed using a shell script, granting Jenkins access to build and run Docker images.

5️⃣ We accessed Jenkins through the browser, installed the required plugins, and created a declarative pipeline to automate the CI/CD process.

6️⃣ The pipeline consisted of stages such as cloning the code, building the image, pushing it to Docker Hub, and deploying the container using Docker Compose.

7️⃣ We discussed additional steps, including adding DockerHub credentials, utilizing a Docker Compose file, and triggering the pipeline with webhooks.

8️⃣ Lastly, we highlighted the benefits of using "Pipeline Script from SCM" to simplify pipeline modifications and encourage team collaboration.

By implementing this Jenkins declarative pipeline configuration, you can streamline your software development process, reduce manual efforts, and achieve faster and more reliable deployments. Embracing automation and cloud technologies allows your team to focus on innovation and delivering high-quality software products.

### **🔍 Checkout GitHub Repository for projects:**

**🔗** [**github.com/sumanprasad007**](http://github.com/sumanprasad007)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689016625237/0440ec2c-de01-4c66-8383-595aef609f08.png?auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

  
#Jenkins #Automation #AWS #DevOps #ContinuousIntegration #Cloud