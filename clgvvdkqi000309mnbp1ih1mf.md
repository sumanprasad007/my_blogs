---
title: "Day - 1: Kubernetes Architecture and Components, Kubernetes Installation and Configuration"
datePublished: Tue Apr 25 2023 06:11:56 GMT+0000 (Coordinated Universal Time)
cuid: clgvvdkqi000309mnbp1ih1mf
slug: day-1-kubernetes-architecture-and-components-kubernetes-installation-and-configuration
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1682402401095/73211497-437d-4464-9cd2-00d31376f0c2.png
tags: linux, aws, developer, devops, beginners

---

# **📍** Introduction:

Kubernetes is an open-source platform that is widely used for container orchestration. It is designed to automate the deployment, scaling, and management of containerized applications. Kubernetes can be used to manage and run applications in a variety of environments, including public, private, and hybrid clouds. Kubernetes provides a rich set of features that help manage the complexity of deploying and managing containerized applications at scale. In this blog, we will explain the Kubernetes architecture and its components.

# **📍** Kubernetes Architecture:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682402969006/722f33a8-8cff-4511-80c0-931c4089a5d2.png align="center")

The Kubernetes architecture consists of two main components: Master Components and Node Components.

# **📍** Master Components:

Master components are the control plane components of Kubernetes that manage the Kubernetes cluster. The master components include:

## **🔹** Kubernetes API Server:

The Kubernetes API Server exposes the Kubernetes API, which is used by clients to interact with the Kubernetes cluster. It is the primary management point for the Kubernetes cluster and is responsible for validating and processing API requests.

## **🔹** etcd:

etcd is a distributed key-value store that stores the configuration data of the Kubernetes cluster. It is used to store the state of the cluster, including the state of all objects (pods, services, deployments, etc.).

## **🔹** Kube-Controller Manager:

The Kube-Controller Manager is responsible for running controllers that are responsible for maintaining the desired state of the Kubernetes cluster. The controllers include the node controller, the replication controller, and the endpoint controller.

## **🔹** Kube-Scheduler:

The Kube-Scheduler is responsible for scheduling the pods on the nodes in the Kubernetes cluster. It uses information about the nodes' available resources and the pod's resource requirements to determine the best node to schedule the pod on.

# **📍** Node Components:

Node components are the worker components of Kubernetes that run on each node in the Kubernetes cluster. The node components include:

Kubelet:

The Kubelet is the primary node agent that communicates with the Kubernetes API server and ensures that the containers are running on the node as expected. It is responsible for starting, stopping, and monitoring the containers on the node.

Container Runtime:

The Container Runtime is the software that runs the containers on the node. Kubernetes supports several container runtimes, including Docker, CRI-O, and containerd.

kube-proxy:

The kube-proxy is responsible for providing network connectivity to the pods running on the node. It does this by creating network rules that allow traffic to be forwarded to the pods.

# **📍** Kubernetes Components:

Kubernetes components can be divided into two categories: Control Plane Components and Worker Nodes Components.

# Control Plane Components:

## **🔹** kube-apiserver:

The kube-apiserver is the main management point for the Kubernetes cluster. It exposes the Kubernetes API, which is used by clients to interact with the Kubernetes cluster.

## **🔹** kube-scheduler:

The kube-scheduler is responsible for scheduling the pods on the nodes in the Kubernetes cluster.

## **🔹** kube-controller-manager:

The kube-controller-manager runs controllers that are responsible for maintaining the desired state of the Kubernetes cluster.

## **🔹** etcd:

etcd is a distributed key-value store that stores the configuration data of the Kubernetes cluster.

## **🔹** cloud-controller-manager:

The cloud-controller-manager is responsible for managing the cloud provider-specific resources in the Kubernetes cluster. It provides a way to integrate with the cloud provider's APIs to manage the cloud resources.

# Worker Node Components:

## **🔹** Nodes:

Nodes are the worker machines that run the containers. They are managed by the Kubernetes master components.

## **🔹** Pods:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682403009258/90f69b4c-fac4-4997-9d5f-30a6afaf8266.png align="center")

Pods are the smallest deployable units in the Kubernetes cluster. They contain one or more containers and are scheduled on nodes.

## **🔹** Container Runtime Engine:

The Container Runtime Engine is responsible for running the containers on the node. Kubernetes supports several container runtimes, including Docker, CRI-O, and containerd.

## **🔹** kubelet:

Kubelet is one of the main components of Kubernetes responsible for managing individual nodes and their containers. It is essentially an agent that runs on each node in the Kubernetes cluster and communicates with the API server to ensure that the containers running on the node are healthy and running as expected.

The kubelet performs several functions, including:

1. Fetching container manifests from the Kubernetes API server.
    
2. Ensuring that the containers described in the manifest are running and healthy.
    
3. Reporting the status of the containers back to the API server.
    
4. Mounting and unmounting volumes as necessary.
    
5. Executing container health checks.
    

## **🔹** kube-proxy

The kube-proxy component is responsible for managing the network proxy between the Kubernetes services and the pods that are running on the worker nodes. The kube-proxy uses various networking modes to ensure that the communication between the pods and services is efficient and reliable.

## **🔹** Container Networking

The container networking component is responsible for ensuring that all the containers running on the worker nodes can communicate with each other and with the external networks. Kubernetes provides several plugins for container networking, including Flannel, Calico, and Weave.

# **📍** Installing kubectl and minikube on Ubuntu:

1. Install kubectl:
    
    ```python
    curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
    sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
    kubectl version
    ```
    
    This downloads the latest stable release of kubectl for Linux amd64 architecture, installs it, and verifies the installation.
    
2. Install minikube:
    
    ```python
    curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
    sudo install minikube-linux-amd64 /usr/local/bin/minikube
    minikube start --driver=docker
    ```
    
    This downloads the latest release of minikube for Linux amd64 architecture, installs it, and starts a single-node Kubernetes cluster using the Docker driver.
    
3. Create a pod configuration file:
    
    ```python
    vi pod.yml
    ```
    
    This opens a new file in the vi text editor.
    
4. Paste the following YAML code into the file and save it:
    
    ```python
    apiVersion: v1
    kind: Pod
    metadata:
      name: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80
    ```
    
    This defines a Kubernetes pod called 'nginx' that runs a container using the nginx:1.14.2 image and exposes port 80.
    
5. Create the pod:
    
    ```python
    kubectl create -f pod.yml
    kubectl get pods
    kubectl get pods -o wide
    ```
    
    This creates the 'nginx' pod using the configuration in the pod.yml file, lists the running pods, and shows additional details about the 'nginx' pod.
    
6. Verify the pod is running:
    
    ```python
    minikube ssh
    curl http://<cluster-ip>:80
    ```
    
    This logs into the minikube VM, where the Kubernetes cluster is running, and uses curl to access the nginx web server running in the 'nginx' pod via the cluster IP address.
    
7. Delete the pod:
    
    ```python
    kubectl delete pod nginx
    ```
    
    This deletes the 'nginx' pod from the Kubernetes cluster.
    

# **📍** Conclusion:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682403069380/cd0cb844-38e9-4355-9332-3dfc4bcf5cfe.png align="center")

In summary, Kubernetes is an open-source container orchestration platform that is widely used in modern software development. Kubernetes makes it easy to deploy, manage, and scale containerized applications across multiple clusters, and it provides a highly scalable and fault-tolerant architecture that can handle complex workloads. By using Kubernetes, developers can focus on building and deploying their applications, while the platform takes care of the underlying infrastructure. With its flexible architecture and broad range of features, Kubernetes is an ideal platform for building modern, cloud-native applications.