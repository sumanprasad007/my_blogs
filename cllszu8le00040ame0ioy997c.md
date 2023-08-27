---
title: "PROJECT - 🚀 Deploying Reddit Clone Web App on Kubernetes Cluster: A Step-by-Step Guide"
datePublished: Sun Aug 27 2023 05:12:05 GMT+0000 (Coordinated Universal Time)
cuid: cllszu8le00040ame0ioy997c
slug: project-deploying-reddit-clone-web-app-on-kubernetes-cluster-a-step-by-step-guide
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1692640935440/f3798f65-7a25-4861-abc5-90e30c64dcea.png
tags: aws, kubernetes, developer, devops, 90daysofdevops

---

## 📍 Introduction:

Container orchestration with Kubernetes has become a standard for deploying and managing applications efficiently. In this detailed guide, we will walk you through the process of deploying a Reddit clone web application onto a Kubernetes cluster hosted on AWS. By following these steps, you will not only learn the deployment process but also gain insights into the power of Kubernetes for managing containerized applications.

### **Step 1: Provision AWS Instances 🌐**

Begin by accessing the AWS console and creating two instances with specific configurations:

* **Deployment Server**:
    
    * AMI: Ubuntu
        
    * Type: t2.medium
        

Ensure that you name these instances accordingly for easy reference.

### **Step 2: Clone the Code📂**

📦 On the machine, clone the codebase of your Reddit clone web application.

Link: [https://github.com/sumanprasad007/reddit-clone-deployed-on-kubernetes-cluster.git](https://github.com/sumanprasad007/reddit-clone-deployed-on-kubernetes-cluster.git)

%[https://github.com/sumanprasad007/reddit-clone-deployed-on-kubernetes-cluster.git] 

### **Step 3: Prerequisites 🛠️**

**On Deployment Server**:

* Update the server: `sudo apt-get update`
    
* Install Docker: `sudo apt-get install` [`docker.io`](http://docker.io) `-y`
    
* Give permission to Docker: `sudo usermod -aG docker $USER && newgrp docker`
    
* Install Minikube and Kubectl:
    
    ```plaintext
    curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
    
    sudo install minikube-linux-amd64 /usr/local/bin/minikube
    
    sudo snap install kubectl — classic
    
    minikube start — driver=docker
    ```
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692641481571/011874b4-eb52-41fe-888a-6cfecdad91be.png align="center")

### **Step 4: Write a Dockerfile for the Project 🐳**

Create a Dockerfile for your Reddit clone project with the following content:

```plaintext
FROM node:19-alpine3.15

WORKDIR /reddit-clone

COPY . /reddit-clone

RUN npm install

EXPOSE 3000

CMD [“npm”,”run”,”dev”]
```

### **Step 5: Build and Push Docker Image 🚀**

Build the Docker image from the Dockerfile using the following command:

```plaintext
docker build . -t sumanprasad007/reddit-clone
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692641645390/87362cbe-53d6-4fa1-932d-72eabff3b598.png align="center")

After building the image, push it to Docker Hub by running:

```plaintext
docker login
# Enter your username and password
docker push sumanprasad007/reddit-clone
```

### **Step 6: Connect to Deployment Server 🖥️**

SSH into the Deployment Server.

### **Step 7: Install Minikube and Kubectl**

Ensure Minikube and Kubectl are installed on the Deployment Server.

### **Step 8: Deploy Docker Image 🚢**

Now, it's time to deploy the Docker image from Docker Hub onto your Kubernetes cluster.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692641677775/008c0f4a-6e7c-402f-9935-c10fd0276b27.png align="center")

### **Step 9: Create a Kubernetes Folder 📁**

Create a folder named "K8s" on the Deployment Server.

### **Step 10: Create a Deployment YAML File 📝**

Inside the "K8s" folder, create a file named "Deployment.yml" and add the following content:

```plaintext
apiVersion: apps/v1
kind: Deployment
metadata:
  name: reddit-clone-deployment
  labels:
    app: reddit-clone
spec:
  replicas: 2
  selector:
    matchLabels:
      app: reddit-clone
  template:
    metadata:
      labels:
        app: reddit-clone
    spec:
      containers:
        - name: reddit-clone
          image: trainwithshubham/reddit-clone
          ports:
            - containerPort: 3000
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692641736372/772cce91-2dfb-4bad-a628-17d1825f35c5.png align="center")

### **Step 11: Apply the Deployment File 📜**

Apply the Deployment file to create pods:

```plaintext
kubectl apply -f Deployment.yml
```

### **Step 12: Verify Deployments 🧐**

To ensure that the deployments are successful, use the following command:

```plaintext
kubectl get deployments
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692641741911/bbea78cd-6bc3-4274-9f1f-11a520d653ea.png align="center")

### **Step 13: Create a Kubernetes Service 🌐**

Now, you need to create a Service to provide an IP address for your application within the cluster.

### **Step 14: Create a Service YAML File 📝**

Inside the "K8s" folder, create a file named "Service.yml" and add the following content:

```plaintext
apiVersion: v1
kind: Service
metadata:
  name: reddit-clone-service
  labels:
    app: reddit-clone
spec:
  type: NodePort
  ports:
    - port: 3000
      targetPort: 3000
      nodePort: 31000
  selector:
    app: reddit-clone
```

### **Step 15: Apply the Service File 📜**

Apply the Service file to create a service:

```plaintext
kubectl apply -f Service.yml
```

### **Step 16: Check the Service 🌐**

To verify that the service is created successfully, run:

```plaintext
kubectl get services
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692641766429/c66262dc-3239-46a8-b2c5-d76603d44d4d.png align="center")

### **Step 17: Access the Application 🚀**

You can now access your application by visiting the URL provided by Minikube:

```plaintext
minikube service reddit-clone-service — url
```

### **Step 18: Expose the Application to the Internet 🌍**

To make your application accessible from the internet, you'll need to configure port forwarding.

### **Step 19: Port Forwarding 🔄**

Run the following command for port forwarding:

```plaintext
kubectl port-forward svc/reddit-clone-service 3000:3000
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692641830306/ce46d285-fd2e-4dc7-89ce-9755dbc11d1d.png align="center")

### **Step 20: Access Your Live Reddit Clone 🌐**

Visit your Reddit Clone web app at the provided domain or IP address, and it should now be accessible to the world.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692641435614/0616bc3a-b6c3-4dce-ac71-72386d8854cd.png align="center")

## 📍 Conclusion

Congratulations! 🎉 You've successfully deployed a Reddit clone web app on a Kubernetes cluster hosted on AWS. This guide has covered the entire process, from provisioning AWS instances to advanced routing using Ingress. Kubernetes offers powerful capabilities for container orchestration, making it an essential tool for modern application deployment and management. Explore the various use cases to adapt this project to your specific needs.

### **🔍 Checkout GitHub Repository for projects:**

**🔗** [**github.com/sumanprasad007**](http://github.com/sumanprasad007)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692607442282/98c6c100-886d-4894-80bc-db5df0141100.png?auto=compress,format&format=webp align="left")

### **🔍 Check out my YouTube channel - Prasad Suman Mohan:**

🔗 [**youtube.com/@sumanprasad007**](http://youtube.com/@sumanprasad007)

%[https://youtu.be/oVJoN5Zc3Kw]