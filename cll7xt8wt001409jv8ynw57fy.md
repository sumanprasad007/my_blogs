---
title: "Kubernetes Cluster Setup with EKS and Kubectl 🚀"
datePublished: Sat Aug 12 2023 11:32:10 GMT+0000 (Coordinated Universal Time)
cuid: cll7xt8wt001409jv8ynw57fy
slug: kubernetes-cluster-setup-with-eks-and-kubectl
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1691839857672/b18da5ad-9c75-4b6f-8182-ac079e2b7a36.png
tags: aws, kubernetes, developer, devops, 90daysofdevops

---

## **📍 Introduction:**

Are you ready to venture into the world of Kubernetes but finding the setup process overwhelming? Fear not! In this guide, we'll take you through the step-by-step process of installing Kubectl and EKS CTL, setting up an EKS cluster, and showcasing real-time examples to illuminate each step. Let's dive in! 🌟

### **Prerequisites:**

1. **AWS EC2 Instance:**
    
    * Launch an EC2 instance on Amazon Web Services (AWS) using the Amazon Linux image.
        
    * Choose the instance type `t2.medium` to ensure sufficient resources for the cluster setup.
        
2. **AWS IAM Role:**
    
    * Create an IAM role named `ec2` with the `AdministratorAccess` policy attached.
        
    * Attach this IAM role to the EC2 instance you launched. This role will grant necessary permissions for the instance to access AWS services.
        

With these prerequisites ready, you're all set to follow the steps in the previous sections to install Kubectl and EKS CTL, create the EKS cluster, add OIDC for Kubernetes, and add nodes to the cluster.

### **Step 1: Installing Kubectl and EKS CTL**

#### **Installing Kubectl**

Kubectl is the command-line tool that lets you interact with Kubernetes clusters. Let's install it:

* Download Kubectl:
    

```plaintext
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
```

* Download Kubectl SHA-256 checksum:
    

```plaintext
curl -LO "https://dl.k8s.io/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl.sha256"
```

* Verify the checksum:
    

```plaintext
echo "$(cat kubectl.sha256) kubectl" | sha256sum --check
```

* Install Kubectl:
    

```plaintext
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
```

* Check if Kubectl is installed:
    

```plaintext
kubectl get pods
```

#### **Installing EKS CTL**

EKS CTL simplifies the process of creating, updating, and managing Amazon EKS clusters. Let's install it:

* Download and install EKS CTL:
    

```plaintext
curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
sudo mv /tmp/eksctl /usr/bin
```

* Verify EKS CTL installation:
    

```plaintext
eksctl version
```

### **Step 2: Adding IAM Role to EC2 Instances**

To enable EC2 instances to access the EKS cluster, you need to attach an IAM role to them:

* Create an IAM role named `ec2` with `AdministratorAccess` policy attached.
    
* Attach the role to your EC2 instances.
    

### **Step 3: Creating the EKS Cluster**

* Create the EKS cluster (This might take 10-15 minutes):
    

```plaintext
eksctl create cluster --name=eksdemo1 --region=us-west-1 --zones=us-west-1b,us-west-1a --without-nodegroup
```

### **Step 4: Adding OIDC for Kubernetes**

OIDC (OpenID Connect) allows Kubernetes to access external resources. Associate the OIDC provider:

```plaintext
eksctl utils associate-iam-oidc-provider --region us-west-1 --cluster eksdemo1 --approve
```

### **Step 5: Adding Nodes to the Cluster**

Let's add nodes to the cluster using EKS CTL:

```plaintext
eksctl create nodegroup --cluster=eksdemo1 --region=us-west-1 --name=eksdemo-ng-public --node-type=t2.medium --nodes=2 --nodes-min=2 --nodes-max=4 --node-volume-size=10 --ssh-access --ssh-public-key=k8-west1 --managed --asg-access --external-dns-access --full-ecr-access --appmesh-access --alb-ingress-access
```

### **Checking Your Progress**

To see all the running pods, execute:

```plaintext
kubectl get pods -n kube-system
```

## **📍Conclusion:**

**Navigating the EKS Galaxy Made Simple**

With Kubectl and EKS CTL in your toolbox, setting up a Kubernetes cluster becomes a breeze. You've journeyed through installation, IAM role setup, EKS cluster creation, OIDC integration, and node addition. As you revel in the thriving Kubernetes ecosystem, remember that mastering these tools opens doors to a universe of efficient and seamless container orchestration. Your Kubernetes odyssey has just begun! 🌌

### **🔍 Checkout GitHub Repository for projects:**

**🔗** [**github.com/sumanprasad007**](http://github.com/sumanprasad007)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690656559825/0474ff76-1d75-4ce0-93ea-1194d2444f74.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

### **🔍 Check out my YouTube channel - Prasad Suman Mohan:**

🔗 [**https://youtu.be/oVJoN5Zc3Kw**](https://youtu.be/oVJoN5Zc3Kw)

%[https://youtu.be/oVJoN5Zc3Kw]