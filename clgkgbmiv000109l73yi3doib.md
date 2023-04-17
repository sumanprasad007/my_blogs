---
title: "🐳 Understanding Docker Networking, Bridge vs Host vs Overlay & Secure containers"
datePublished: Mon Apr 17 2023 06:25:03 GMT+0000 (Coordinated Universal Time)
cuid: clgkgbmiv000109l73yi3doib
slug: understanding-docker-networking-bridge-vs-host-vs-overlay-secure-containers
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1681712541175/c31e769d-83dc-43dd-a3de-259a3c485e6d.png
tags: linux, aws, developer, devops, beginners

---

# **📍 Introduction:**

If you're interested in working with containers and container orchestration tools like Kubernetes and Docker Swarm, it's important to understand networking in Docker. Docker networking is a critical component that allows containers to communicate with each other and with other resources on a network.

In this blog post, we'll explore the basics of Docker networking and cover some key concepts that you'll need to know to work effectively with containers and container orchestration tools.

## **🔹** Why do you need networking on Docker? 🤔

Docker networking is essential for allowing containers to communicate with each other and with other resources on a network. For example, if you have multiple containers running on the same host, they need to be able to communicate with each other to function properly.

## **🔹** How does Docker Networking Work? 🛠️

Docker networking works by creating a virtual network that allows containers to communicate with each other and with other resources on a network. Each container is assigned an IP address within the virtual network, and Docker provides a range of networking options to allow containers to communicate with each other and with other resources on the network.

## **🔹** What are the different types of Networking in Docker? 🌐

Docker provides several different types of networking options, including bridge networks, host networks, overlay networks, and macvlan networks.

### ⚜ Example of creating a bridge network:

```python
docker network create --driver bridge my-network
```

## **🔹** Which Networking is default and Out of the Box? 🔍

Bridge networks are the default networking option in Docker and are included out of the box. They are the most commonly used networking option in Docker and provide a private network that is isolated from the host system and other networks.

## **🔹** Play with Docker containers and inspect their Networks 🐋

To get a better understanding of Docker networking, it's useful to experiment with containers and inspect their networks. Docker provides a range of commands that allow you to create and manage containers, as well as inspect their networks.

### ⚜ Example of listing available networks in Docker:

```python
docker network ls
```

## **🔹** Create a custom bridge network to secure it from other containers 🔒

If you need to create a custom network in Docker, you can use the "docker network create" command to create a new network. This can be useful if you need to secure a network and prevent other containers from accessing it.

### ⚜ Example of creating a custom bridge network:

```python
docker network create --driver bridge my-secure-network
```

# **📍** Conclusion:

In conclusion, understanding Docker networking is essential if you want to work effectively with containers and container orchestration tools like Kubernetes and Docker Swarm. By exploring the basics of Docker networking and experimenting with containers, you can gain a better understanding of how networking works in Docker and how to use it effectively in your container deployments.

# **📍 Resources:**

%[https://youtu.be/xrUGEoUpa3s?list=PLdpzxOOAlwvIKMhk8WhzN1pYoJ1YU8Csa] 

```python
I invite you to check my portfolio in case you are interested in contacting me for a project!. Prasad Suman Mohan

🔵 Don't forget to follow me also on LinkedIn: https://www.linkedin.com/in/prasad-suman-mohan
```