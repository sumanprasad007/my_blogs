---
title: "Kubernetes Pods & Deploy Your First App"
datePublished: Mon Apr 24 2023 13:53:54 GMT+0000 (Coordinated Universal Time)
cuid: clguwftjt000109la00v5ffje
slug: kubernetes-pods-deploy-your-first-app
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1682344260081/a3a063ae-0c37-41e0-b4c7-0914488b1126.webp
tags: linux, aws, developer, devops, beginners

---

# **📍 Introduction:**

In this blog, you will learn about Kubernetes pods, which are the smallest deployable units in Kubernetes. You will learn the differences between containers and pods, how to install kubectl and Minikube, and how to create and write your first Pod. Additionally, you will discover the advantages of using Pods in Kubernetes.

## **🔹** Container vs Pod:

Containers are standalone executable packages of software that include everything needed to run an application, including code, libraries, and system tools. A Pod is the smallest deployable unit in Kubernetes, and it is a logical host for one or more containers. A Pod can contain one or more containers, and those containers share the same network namespace, and they can also share the same storage volumes.

## **🔹** What is Kubectl && Installation:

Kubectl is a command-line tool for Kubernetes that allows you to deploy and manage applications on a Kubernetes cluster. You can install Kubectl on your local machine by following the instructions on the Kubernetes documentation. Here is an example of how to install Kubectl on Ubuntu:

```python
$ sudo apt-get update && sudo apt-get install -y apt-transport-https gnupg2
$ curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
$ echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list
$ sudo apt-get update
$ sudo apt-get install -y kubectl
```

## **🔹** Minikube Installation:

Minikube is a tool that allows you to run a Kubernetes cluster on your local machine. You can install Minikube by following the instructions on the Kubernetes documentation. Here is an example of how to install Minikube on Ubuntu:

```python
$ curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
$ sudo install minikube-linux-amd64 /usr/local/bin/minikube
```

## **🔹** How to create a Pod:

You can create a Pod using the `kubectl create` command. Here is an example of how to create a Pod:

```python
$ kubectl create pod nginx --image=nginx
```

## **🔹** How to write your first Pod:

You can write your first Pod using a YAML file. Here is an example of a YAML file that defines a Pod with a single container:

```python
apiVersion: v1
kind: Pod
metadata:
  name: nginx
spec:
  containers:
  - name: nginx
    image: nginx
```

You can create the Pod using the `kubectl apply` command:

```python
$ kubectl apply -f pod.yaml
```

# **📍** Advantages of Pods: Pods provide several advantages, including:

* Simplified networking: Containers within a Pod can communicate over [localhost](http://localhost), which eliminates the need for complex networking configurations and enables easy service discovery and load balancing.
    
* Shared resources: Pods can share storage volumes, environment variables, and secrets, which enables data sharing and coordination between containers.
    
* Atomic scheduling: Pods are the smallest unit of deployment in Kubernetes and can be scheduled and replicated atomically, which ensures high availability and fault tolerance.
    
* Sidecar containers: Pods can include sidecar containers that provide additional functionality, such as logging, monitoring, or networking, which enhances the capabilities and resilience of the application.
    
* Blue-green deployment: Pods can be used for blue-green or canary deployments, where a new version of the application is deployed to a new set of Pods and then gradually phased in, while the old version is phased out, which reduces the risk and downtime of the deployment.
    
* Scaling: Pods can be scaled horizontally or vertically by adding or removing replicas or adjusting the resource limits of the containers, which enables efficient resource utilization and responsiveness.
    
* They provide a logical host for one or more containers, which allows you to group related containers together and manage them as a single unit.
    
* They share the same network namespace, which allows containers within a Pod to communicate with each other using [`localhost`](http://localhost).
    
* They can share the same storage volumes, which allows containers within a Pod to share data.
    
* They can be easily scaled horizontally by creating multiple replicas of the same Pod.
    

# **📍** Conclusion:

Kubernetes Pods provide a powerful abstraction for deploying and managing containerized applications in a scalable, flexible, and resilient way. By using Pods, you can simplify networking, share resources, ensure atomic scheduling, enable co-located and sidecar containers, support blue-green deployment, and achieve efficient scaling. With the knowledge and skills gained from this tutorial, you can start building and running your own Kubernetes Pods and take your container orchestration to the next level.