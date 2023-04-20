---
title: "Understanding Kubernetes Architecture Comparison with Docker Architecture"
datePublished: Thu Apr 20 2023 05:45:27 GMT+0000 (Coordinated Universal Time)
cuid: clgop89bn000009la5v7q1ev5
slug: understanding-kubernetes-architecture-comparison-with-docker-architecture
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1681968937834/477000d1-50f5-472a-965d-8cbcb9f4c912.webp
tags: linux, aws, developer, devops, beginners

---

# **📍 Introduction:**

Kubernetes is a powerful container orchestration system that can help simplify the deployment and management of containerized applications. In this article, we'll explore the architecture of Kubernetes, including its control plane, data plane, and various components. Let's first discuss what's the main difference between the architecture of Kubernetes and Docker is?

# **📍** Kubernetes vs Docker Architecture

While Docker focuses on creating and managing containers, Kubernetes focuses on orchestrating and managing containerized applications. The main difference between Docker and Kubernetes architecture is that Docker architecture consists of a single host machine that runs the containers, while Kubernetes architecture consists of a cluster of worker machines that run the containers.

## **🔹 Examples**

Let’s take an example of deploying a simple web application to understand the difference between Docker and Kubernetes architecture.

In Docker architecture, we need to create a Dockerfile that contains the instructions to build the Docker image of the web application. Once the Docker image is built, we can run it on a Docker host using the Docker run command.

In Kubernetes architecture, we need to create a YAML file that describes the deployment of the web application. The YAML file contains information such as the number of replicas of the web application, the container image to use, and the port to expose. Once the YAML file is created, we can use the kubectl command to deploy the web application to the Kubernetes cluster.

# **📍** Kubernetes Control Plane:

The Kubernetes control plane is responsible for managing the overall state of the cluster. It includes several components, each of which performs a specific function.

The components of the Kubernetes control plane include:

## **🔹** API Server:

This component serves as the primary interface for the control plane, and exposes the Kubernetes API.

## **🔹** etcd:

This is a distributed key-value store that is used to store the cluster's state.

## **🔹** Controller Manager:

This component is responsible for managing various controllers that watch for changes in the cluster's state and take appropriate action.

## **🔹** Scheduler:

This component is responsible for scheduling workloads onto nodes in the cluster.

# **📍** Kubernetes Data Plane:

The Kubernetes data plane is responsible for handling network traffic between the various components of the cluster. It includes several components, each of which performs a specific function.

The components of the Kubernetes data plane include:

## **🔹** Kubelet:

This component runs on each node in the cluster, and is responsible for managing the containers running on that node.

## **🔹** Kube-proxy:

This component is responsible for handling network traffic to and from the containers running on each node.

## **🔹** Container Runtime:

This is the software that actually runs the containers on each node.

## **🔹** Kubernetes Components with Examples Kubernetes

It includes a variety of components that work together to provide a powerful container orchestration system. Here are a few examples of some of the most important components:

* Pod: A pod is the smallest deployable unit in Kubernetes. It consists of one or more containers that share network and storage resources.
    
* Deployment: A deployment is used to manage the rollout and scaling of a set of replicas (pods).
    
* Service: A service is used to expose a set of pods to the network, and provides a stable IP address and DNS name for accessing the pods.
    
* Ingress: An ingress is used to expose HTTP and HTTPS routes from outside the cluster to services within the cluster.
    
* ConfigMap: A ConfigMap is used to store configuration data that can be accessed by containers running within a pod.
    
* Secret: A Secret is used to store sensitive data, such as passwords or API keys, that can be accessed by containers running within a pod.
    

# **📍 Conclusion:**

In conclusion, Kubernetes is a powerful container orchestration system that includes a variety of components that work together to provide a powerful and flexible platform for deploying and managing containerized applications. By understanding the architecture of Kubernetes, including its control plane, data plane, and various components, you can better understand how to deploy and manage your applications in a Kubernetes cluster.

# **📍 Resources:**

%[https://youtu.be/gywke3XiNC0?list=PLdpzxOOAlwvIKMhk8WhzN1pYoJ1YU8Csa] 

```python
I invite you to check my portfolio in case you are interested in contacting me for a project!. Prasad Suman Mohan

🔵 Don't forget to follow me also on LinkedIn: https://www.linkedin.com/in/prasad-suman-mohan
```