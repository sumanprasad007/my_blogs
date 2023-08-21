---
title: "Simplifying Kubernetes Cluster Setup with Kubeadm Installation Guide 🚀"
datePublished: Sun Aug 20 2023 16:31:54 GMT+0000 (Coordinated Universal Time)
cuid: clljo1ir3000109jvdvpj4kn7
slug: simplifying-kubernetes-cluster-setup-with-kubeadm-installation-guide
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1692548658498/39c32299-5472-4bdf-a82c-07d419183afd.png
tags: aws, kubernetes, developer, devops, 90daysofdevops

---

# **📍 Introduction:**

In the world of container orchestration, Kubernetes has emerged as the de facto standard. It provides a powerful platform for managing containerized applications, but setting up a Kubernetes cluster can be a daunting task. That's where Kubeadm comes to the rescue. In this guide, we'll walk you through the process of setting up a Kubernetes cluster using Kubeadm on Ubuntu.

### **🔍 Prerequisites** ✅

Before we dive into the installation process, let's make sure we have everything we need:

* **Ubuntu OS (Xenial or later):** We'll use Ubuntu as our operating system.
    
* **sudo privileges:** You need administrative access to the servers.
    
* **Internet access:** To download necessary packages.
    
* **t2.medium instance type or higher:** This guide assumes you have access to suitable hardware.
    
* **Both Master & Worker Node:** For a fully functional cluster.
    

### **🔍 Installation Steps** 🛠️

1. **Update and Install Docker** 🐳
    
    * Run the following commands on both the master and worker nodes to prepare them for Kubeadm:
        
        ```plaintext
        sudo su
        apt update -y
        apt install docker.io -y
        systemctl start docker
        systemctl enable docker
        ```
        
        Kubernetes relies on Docker containers, so it's essential to have Docker installed and running on all nodes.
        
2. **Add Kubernetes Repository and Install Kubeadm** 📦
    
    * To add the Kubernetes repository and install Kubeadm, Kubectl, and Kubelet components, execute:
        
        ```plaintext
        curl -fsSL "https://packages.cloud.google.com/apt/doc/apt-key.gpg" | sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/kubernetes-archive-keyring.gpg
        echo 'deb https://packages.cloud.google.com/apt kubernetes-xenial main' > /etc/apt/sources.list.d/kubernetes.list
        
        apt update -y
        apt install kubeadm=1.20.0-00 kubectl=1.20.0-00 kubelet=1.20.0-00 -y
        ```
        
3. **Initialize the Kubernetes Master Node** 🚀
    
    * Run this command to initialize the Kubernetes control plane on the master node:
        
        ```plaintext
        sudo su
        kubeadm init
        ```
        
4. **Set Up Local Kubeconfig** 📝
    
    * To interact with the Kubernetes cluster from your local machine, create the Kubeconfig file:
        
        ```plaintext
        mkdir -p $HOME/.kube
        sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
        sudo chown $(id -u):$(id -g) $HOME/.kube/config
        ```
        
5. **Apply Weave Network Plugin** 🌐
    
    * Use this command to apply the Weave network plugin, which ensures pod-to-pod communication:
        
        ```plaintext
        kubectl apply -f https://github.com/weaveworks/weave/releases/download/v2.8.1/weave-daemonset-k8s.yaml
        ```
        
6. **Generate Token for Worker Nodes** 🤖
    
    * Generate a token for worker nodes to join the cluster:
        
        ```plaintext
        kubeadm token create --print-join-command
        ```
        
7. **Expose Port 6443 for Worker Node Connectivity** 🔗
    
    * Ensure that port 6443 is accessible from your worker nodes to the master node. This is essential for the worker nodes to communicate with the control plane.
        

### **🔍 Worker Node Setup** 🏗️

1. **Reset Kubeadm and Join Worker Node** 🔄
    
    * On the worker node, execute the following commands:
        
        ```plaintext
        sudo su
        kubeadm reset pre-flight checks
        ```
        
        Then, paste the join command you obtained from the master node during token creation and append `--v=5` for verbose output:
        
        ```plaintext
        kubeadm join <master-node-ip>:6443 --token <token> --discovery-token-ca-cert-hash <hash> --v=5
        ```
        
2. **Verification** ✔️
    
    * On the master node, run:
        
        ```plaintext
        kubectl get nodes
        ```
        
        This should display both the master and worker nodes as part of your Kubernetes cluster.
        

### **🔍 Optional Steps** 🧐

* **Labeling Nodes** 🏷️: If you want to label your worker nodes for specific roles, you can use the following command:
    
    ```plaintext
    kubectl label node <node-name> node-role.kubernetes.io/worker=worker
    ```
    
* **Testing a Demo Pod** 🚀: To verify your cluster's functionality, you can deploy a demo pod:
    
    ```plaintext
    kubectl run nginx --image=nginx --port=80
    kubectl expose pod nginx --port=80 --type=NodePort
    ```
    
* Enable the port range 30000-32767 for the node-port on worker node
    
* Now, type the below command to know the node-port for the pod
    

```plaintext
kubectl get svc
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692548867963/ca862ba3-bddf-4f7a-a36e-168f4888f07a.png align="center")

* Node copy the public-ip of workernode: nodeport in the browser to get the nginx output
    
* ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692548943101/e11dc999-fc1c-487c-8082-15979a56a41c.png align="center")
    
    This will run a simple pod:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692548723166/c238dae0-70a7-4779-8336-65b726a939aa.png align="center")

# 📍Conclusion:

Congratulations! You've successfully set up a Kubernetes cluster using Kubeadm on Ubuntu. This provides you with a powerful platform for deploying and managing containerized applications in a scalable and efficient manner. 🎉

### **🔍 Checkout GitHub Repository for projects:**

**🔗** [**github.com/sumanprasad007**](http://github.com/sumanprasad007)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692607442282/98c6c100-886d-4894-80bc-db5df0141100.png align="center")

### **🔍 Check out my YouTube channel - Prasad Suman Mohan:**

🔗 [**youtube.com/@sumanprasad007**](http://youtube.com/@sumanprasad007)

%[https://youtu.be/oVJoN5Zc3Kw]