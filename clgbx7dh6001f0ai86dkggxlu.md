---
title: "Docker Zero to Hero: Streamlining Development and Deployment of Applications"
datePublished: Tue Apr 11 2023 07:07:42 GMT+0000 (Coordinated Universal Time)
cuid: clgbx7dh6001f0ai86dkggxlu
slug: docker-zero-to-hero-streamlining-development-and-deployment-of-applications
tags: linux, aws, developer, devops, beginners

---

# **📍 Introduction:**

Docker is an open-source platform that allows developers to build, ship, and run applications as containers. It is a lightweight and portable containerization technology that packages an application and all its dependencies in a container, which can be easily deployed on any host system.

In this blog, we will discuss the basic concepts of Docker, including what containers are, how they differ from virtual machines, and how Docker works. We will also explore the Docker architecture and look at some code examples that demonstrate how to use Docker.

## **🔹** What is a container?

A container is a standard unit of software that packages up code and all its dependencies so that the application runs quickly and reliably from one computing environment to another. It includes everything needed to run an application, including code, runtime, system tools, system libraries, and settings.

In simpler terms, a container is a bundle of an application, application libraries, and the minimum system dependencies required to run the application. Containers are designed to be lightweight and portable, which makes them ideal for deployment across various environments, including development, testing, and production.

## **🔹** Containers vs Virtual Machines:

![](https://user-images.githubusercontent.com/43399466/217262726-7cabcb5b-074d-45cc-950e-84f7119e7162.png align="left")

Containers and virtual machines (VMs) are both technologies used to isolate applications and their dependencies. However, there are some key differences between the two:

1. Resource Utilization: Containers share the host operating system kernel, making them lighter and faster than VMs. VMs, on the other hand, have a full-fledged operating system and hypervisor, making them more resource-intensive.
    
2. Portability: Containers are designed to be portable and can run on any system with a compatible host operating system. VMs are less portable as they require a compatible hypervisor to run.
    
3. Security: VMs provide a higher level of security as each VM has its operating system and can be isolated from the host and other VMs. Containers provide less isolation, as they share the host operating system.
    
4. Management: Managing containers is typically easier than managing VMs, as containers are designed to be lightweight and fast-moving.
    

## **🔹** Why are containers lightweight?

Containers are lightweight because they use a technology called containerization, which allows them to share the host operating system's kernel and libraries while still providing isolation for the application and its dependencies. This results in a smaller footprint compared to traditional virtual machines, as containers do not need to include a full operating system. Additionally, Docker containers are designed to be minimal, only including what is necessary for the application to run, further reducing their size.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681195571039/617e766a-dc9e-4e59-beb3-d6423ee768c2.png align="center")

# **📍** Docker Architecture:

The Docker architecture consists of a client-server architecture with the following components:

1. Docker Client: This is a command-line interface (CLI) tool that sends commands to the Docker daemon.
    
2. Docker Daemon: This is the server component that manages Docker objects, including images, containers, networks, and volumes.
    
3. Docker Registry: This is a central repository that stores Docker images.
    

Image Source: [**https://docs.docker.com/engine/docker-overview/**](https://docs.docker.com/engine/docker-overview/)

![](https://user-images.githubusercontent.com/43399466/217507877-212d3a60-143a-4a1d-ab79-4bb615cb4622.png align="left")

# **📍** How to use Docker?

Using Docker involves the following steps:

1. Create a Dockerfile: A Dockerfile is a text file that contains instructions for building a Docker image. The instructions specify the base image to use, any additional software to install, and the commands to run when the container is started.
    
2. Build the Docker image: The Dockerfile is used to build a Docker image, which is a read-only template used to create a container.
    
3. Run the Docker container: The Docker image is used to create a Docker container, which is a running instance of the image. Containers can be started, stopped, and deleted as needed.
    
4. Push the Docker image: Once the Docker image is built, it can be pushed to a Docker registry, such as DockerHub or [Quay.io](http://Quay.io), where it can be shared with others.
    

### **🔹**Docker LifeCycle

We can use the above Image as a reference to understand the lifecycle of Docker.

There are three important things,

1. docker build -&gt; builds docker images from Dockerfile
    
2. docker run -&gt; runs container from docker images
    
3. docker push -&gt; push the container image to public/private registries to share the docker images.
    

[![Screenshot 2023-02-08 at 4 32 13 PM](https://user-images.githubusercontent.com/43399466/217511949-81f897b2-70ee-41d1-b229-38d0572c54c7.png align="left")](https://user-images.githubusercontent.com/43399466/217511949-81f897b2-70ee-41d1-b229-38d0572c54c7.png)

# **📍** Understanding the terminology (Inspired by Docker Docs)

### **🔹** Docker daemon

The Docker daemon (docked) listens for Docker API requests and manages Docker objects such as images, containers, networks, and volumes. A daemon can also communicate with other daemons to manage Docker services.

### **🔹** Docker client

The Docker client (docker) is the primary way that many Docker users interact with Docker. When you use commands such as docker run, the client sends these commands to docker, which carries them out. The docker command uses the Docker API. The Docker client can communicate with more than one daemon.

### **🔹** Docker Desktop

Docker Desktop is an easy-to-install application for your Mac, Windows or Linux environment that enables you to build and share containerized applications and microservices. Docker Desktop includes the Docker daemon (docked), the Docker client (docker), Docker Compose, Docker Content Trust, Kubernetes, and Credential Helper. For more information, see Docker Desktop.

### **🔹** Docker registries

A Docker registry stores Docker images. Docker Hub is a public registry that anyone can use, and Docker is configured to look for images on Docker Hub by default. You can even run your private registry.

When you use the docker pull or docker run commands, the required images are pulled from your configured registry. When you use the docker push command, your image is pushed to your configured registry. Docker objects

When you use Docker, you are creating and using images, containers, networks, volumes, plugins, and other objects. This section is a brief overview of some of those objects.

### **🔹** Dockerfile

Dockerfile is a file where you provide the steps to build your Docker Image.

### **🔹** Docker Image

An image is a read-only template with instructions for creating a Docker container. Often, an image is based on another image, with some additional customization. For example, you may build an image which is based on the Ubuntu image but installs the Apache web server and your application, as well as the configuration details needed to make your application run.

You might create your images or you might only use those created by others and published in a registry. To build your image, you create a Dockerfile with a simple syntax for defining the steps needed to create the image and run it. Each instruction in a Dockerfile creates a layer in the image. When you change the Dockerfile and rebuild the image, only those layers which have changed are rebuilt. This is part of what makes images so lightweight, small, and fast when compared to other virtualization technologies.

# **📍** INSTALL DOCKER

Very detailed instructions to install Docker are provided in the below link

[https://docs.docker.com/get-docker/](https://docs.docker.com/get-docker/)

For Demo, You can create an Ubuntu EC2 Instance on AWS and run the below commands to install docker.

```python
sudo apt update
sudo apt install docker.io -y
```

### **🔹** Start Docker and Grant Access

A very common mistake that many beginners do is, After they install docker using the sudo access, they miss the step to Start the Docker daemon and grant access to the user they want to use to interact with docker and run docker commands.

Always ensure the docker daemon is up and running.

An easy way to verify your Docker installation is by running the below command

```python
docker run hello-world
```

If the output says:

```python
docker: Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Post "http://%2Fvar%2Frun%2Fdocker.sock/v1.24/containers/create": dial unix /var/run/docker.sock: connect: permission denied.
See 'docker run --help'.
```

This can mean two things,

1. The Docker daemon is not running.
    
2. Your user does not have access to run docker commands.
    

### **🔹** Start Docker daemon

You use the below command to verify if the docker daemon is started and Active

```python
sudo systemctl status docker
```

If you notice that the docker daemon is not running, you can start the daemon using the below command

```python
sudo systemctl start docker
```

### **🔹** Grant Access to your user to run docker commands

To grant access to your user to run the docker command, you should add the user to the Docker Linux group. A Docker group is created by default when Docker is installed.

```python
sudo usermod -aG docker ubuntu
```

In the above command, `ubuntu` is the name of the user, you can change the username appropriately.

**NOTE:**: You need to log out and log in back for the changes to be reflected.

### **🔹** Docker is Installed, up and running 🥳🥳

Use the same command again, to verify that docker is up and running.

```python
docker run hello-world
```

The output should look like this:

```python
Hello from Docker!
This message shows that your installation appears to be working correctly.
```

### **🔹** Clone this repository and move it to the example folder

```python
git clone https://github.com/iam-veeramalla/Docker-Zero-to-Hero
cd  examples
```

### **🔹** Log in to Docker \[Create an account with [**https://hub.docker.com/**](https://hub.docker.com/)**\]**

```python
docker login
```

```python
Login with your Docker ID to push and pull images from Docker Hub. If you don't have a Docker ID, head over to https://hub.docker.com to create one.
Username: sumanprasad007
Password:
WARNING! Your password will be stored unencrypted in /home/ubuntu/.docker/config.json.
Configure a credential helper to remove this warning. See
https://docs.docker.com/engine/reference/commandline/login/#credentials-store

Login Succeeded
```

### **🔹** Build your first Docker Image

You need to change the username accordingly in the below command

```python
docker build -t sumanprasad007/my-first-docker-image:latest .
```

The output of the above command

```python
    Successfully built 690s22345msdf
    Successfully tagged sumanprasad007/my-first-docker-image:latest
```

### **🔹** Verify Docker Image is created

```python
docker images
```

Output

```python
REPOSITORY                         TAG       IMAGE ID       CREATED          SIZE
sumanprasad007/my-first-docker-image   latest    960d37536dcd   58 seconds ago   467MB
hello-world                        latest    feb5d9fea6a5   14 months ago    13.3kB
```

### **🔹** Run your First Docker Container

```python
docker run -it sumanprasad007/my-first-docker-image
```

Output

```python
Hello World
```

### **🔹** Push the Image to DockerHub and share it with the world

```python
docker push sumanprasad007/my-first-docker-image
```