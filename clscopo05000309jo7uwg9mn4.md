---
title: "Docker Cheat Sheet 🐳: A Guide for DevOps Engineers"
datePublished: Thu Feb 08 2024 03:54:13 GMT+0000 (Coordinated Universal Time)
cuid: clscopo05000309jo7uwg9mn4
slug: docker-cheat-sheet-a-guide-for-devops-engineers
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1707364282995/10c13442-981d-4386-b589-2efe31594b7c.png
tags: tutorial, docker, java, technology, python, web-development, kubernetes, webdev, developer, devops, containers, technical-writing-1, docker-images, 90daysofdevops, trainwithshubham

---

## Introduction

Docker commands are the building blocks for managing containers efficiently. This cheat sheet progresses from basic to advanced commands, providing real-time examples for a comprehensive understanding.

<div data-node-type="callout">
<div data-node-type="callout-emoji">💡</div>
<div data-node-type="callout-text">Download the Docker Cheat Sheet from below<a target="_blank" rel="noopener noreferrer nofollow" href="https://www.linkedin.com/posts/prasad-suman-mohan_docker-cheat-sheet-a-guide-for-devops-activity-7161206554610827264-4Z95?utm_source=share&amp;utm_medium=member_desktop" style="pointer-events: none"> link:</a></div>
</div>

%[https://www.linkedin.com/posts/prasad-suman-mohan_docker-cheat-sheet-a-guide-for-devops-activity-7161206554610827264-4Z95?utm_source=share&utm_medium=member_desktop] 

---

## Basic Container Management 🚢

### 1\. Show Running Containers

```plaintext
docker ps
```

**Example:** Display currently running containers.

### 2\. Stop a Docker Container

```plaintext
docker stop <container name>
```

**Example:** Halt a running container gracefully.

### 3\. Run a Docker Image

```plaintext
docker run <image name>
```

**Example:** Execute a Docker image.

### 4\. View Console Output

```plaintext
docker logs <container name>
```

**Example:** Check the console output of a Docker container.

---

## Intermediate Container Operations 🔄

### 5\. Delete Stopped Containers

```plaintext
docker rm $(docker ps -a -q)
```

**Example:** Clean up stopped containers.

### 6\. Delete All Images

```plaintext
docker rmi $(docker images -q)
```

**Example:** Remove all Docker images on your system.

### 7\. SSH into a Running Container

```plaintext
sudo docker exec -it <container name> bash
```

**Example:** Access a bash shell in a running container.

### 8\. Map Host Port to Container Port

```plaintext
docker run -p <host port>:<container port> <image name>
```

**Example:** Define port mappings for a Docker container.

---

## Advanced Docker Compose and Maven Integration 🔄🛠️

### 9\. Docker Compose Build

```plaintext
docker-compose build
```

**Example:** Build containers defined in `docker-compose.yml`.

### 10\. Docker Compose Start

```plaintext
docker-compose up -d
```

**Example:** Start containers in detached mode.

### 11\. Rebuild and Restart with Docker Compose

```plaintext
docker-compose stop -t 1
docker-compose rm -f
docker-compose pull
docker-compose build
docker-compose up -d
```

**Example:** Stop, remove, pull, rebuild, and restart containers.

### 12\. Maven Build with Docker

```plaintext
mvn clean package docker:build
```

**Example:** Build a Docker image using Maven.

### 13\. Maven Docker Plugin Commands

```plaintext
mvn docker:start
mvn docker:stop
mvn docker:push
mvn docker:run
```

**Example:** Control Docker containers through Maven.

---

## Docker Swarm: Scaling Containers 🐝

### 14\. Initialize Docker Swarm

```plaintext
docker swarm init
```

**Example:** Enable Docker Swarm on the first node.

### 15\. Add a Node to Swarm Cluster

```plaintext
docker swarm join --token <token> --listen-addr <ip:port>
```

**Example:** Expand the Swarm cluster with a new node.

### 16\. List Swarm Nodes and Services

```plaintext
docker node ls
docker service ls
```

**Example:** View nodes and services in the Swarm.

---

## Real-time Scenarios 🎉

* **🚢 Basic Operations:** Display running containers, stop, run, and check logs.
    
* ```plaintext
      docker ps
      docker stop <container name>
      docker run <image name>
      docker logs <container name>
    ```
    
* **🔄 Intermediate Actions:** Remove stopped containers, delete images, access a running container, and define port mappings.
    
* ```plaintext
      docker rm $(docker ps -a -q)
      docker rmi $(docker images -q)
      sudo docker exec -it <container name> bash
      docker run -p <host port>:<container port> <image name>
    ```
    
* **🔄🛠️ Docker Compose and Maven:** Build, start, stop, push, and run containers with Docker Compose and Maven.
    
* ```plaintext
      docker-compose build
      docker-compose up -d
      mvn clean package docker:build
      mvn docker:start
    ```
    
* **🐝 Docker Swarm Scaling:** Initialize Swarm, add a node, and list nodes and services.
    
* ```plaintext
      docker swarm init
      docker swarm join --token <token> --listen-addr <ip:port>
      docker node ls
      docker service ls
    ```
    

## Docker Networking and Port Mapping 🌐

### 17\. Share Storage with a Container

```plaintext
docker run -v <host path>:<container path> <image name>
```

**Example:** Share storage between a host system and a Docker container.

### 18\. Map Host Port to Container Port

```plaintext
docker run -p <host port>:<container port> <image name>
```

**Example:** Define port mappings for a Docker container.

---

## Advanced Dockerfile Configurations ⚙️

### 19\. Adding Oracle Java to an Image

```plaintext
# Example Dockerfile snippet
FROM centos:latest

ENV JAVA_VERSION 8u31
ENV BUILD_VERSION b13

# Upgrading system
RUN yum -y upgrade
RUN yum -y install wget
# ... (rest of the Java installation steps)
```

**Example:** Incorporate Oracle Java into your Docker image.

### 20\. Adding a Spring Boot Executable JAR to an Image

```plaintext
# Example Dockerfile snippet
FROM openjdk:8-jre-alpine

ADD /maven/myapp-0.0.1-SNAPSHOT.jar myapp.jar
RUN sh -c 'touch /myapp.jar'

ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom","-jar","/myapp.jar"]
```

**Example:** Prepare a Docker image for a Spring Boot application.

---

## Docker Commands with Emoji Usage 🎉

* **🚮 Cleaning Up:** Use delete commands with emojis for easy identification.
    
* ```plaintext
      docker rm $(docker ps -a -q)
    ```
    
* **🔄 Automation:** Employ Docker Compose and Maven commands for seamless automation.
    
* ```plaintext
      docker-compose up -d
      mvn clean package docker:build
    ```
    
* **🛠️ Dockerizing Apps:** Utilize Java and Spring Boot examples for adding functionalities to Docker images.
    
* ```plaintext
      ADD /maven/myapp-0.0.1-SNAPSHOT.jar myapp.jar
    ```
    
* **🏃‍♂️ Daily Use Commands:** Run, stop, and view logs with emojis for quick recognition.
    
* ```plaintext
      docker stop <container name>
    ```
    
* **🌐 Networking:** Port mapping and volume sharing commands with emojis for clarity.
    
* ```plaintext
      docker run -p <host port>:<container port> <image name>
    ```
    
* **🔄 Maven Integration:** Maven commands with emojis for building, starting, stopping, and pushing Docker images.
    
* ```plaintext
      mvn clean package docker:build
      mvn docker:start
    ```
    
* **🐝 Docker Swarm:** Swarm commands annotated with emojis for initiation, node management, and service handling.
    
* ```plaintext
      docker swarm init
      docker node ls
    ```
    

---

## Real-world Use Cases 🌍

### 21\. Continuous Integration with Jenkins

```plaintext
docker-compose stop -t 1
docker-compose rm -f
docker-compose pull
docker-compose build
docker-compose up -d
```

**Scenario:** CI builds with Jenkins, ensuring the latest artifacts are used.

### 22\. Multi-environment Deployment

```plaintext
docker run -p 8080:8080 <image name>
```

**Scenario:** Deploying applications on different environments using port mapping.

### 23\. Dynamic Scaling in Cloud Environments

```plaintext
docker service ls
docker service rm <service name>
```

**Scenario:** Scaling services dynamically in a cloud environment using Docker Swarm.

### 24\. Efficient Resource Utilization

```plaintext
docker-compose logs -f
```

**Scenario:** Real-time monitoring of container logs for resource utilization analysis.

---

## Conclusion

This extended Docker cheat sheet covers a range of commands, from basic container management to advanced Dockerfile configurations and real-world use cases. Whether you are a beginner or an experienced DevOps engineer, these commands and examples will enhance your Docker proficiency. Happy Dockerizing! 🐳🚀