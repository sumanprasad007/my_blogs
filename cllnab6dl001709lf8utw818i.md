---
title: "🌐 Deploying a Production-Ready Web App using Docker Swarm on AWS"
datePublished: Wed Aug 23 2023 05:18:34 GMT+0000 (Coordinated Universal Time)
cuid: cllnab6dl001709lf8utw818i
slug: deploying-a-production-ready-web-app-using-docker-swarm-on-aws
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1692708499708/5d802189-0a6f-40fc-91a4-efd081fdb07c.png
tags: docker, aws, developer, devops, 90daysofdevops

---

# **📍** Introduction

Containerization has revolutionized the way applications are deployed and managed, and Docker Swarm is a powerful tool for orchestrating containers in a production environment. In this step-by-step guide, we will walk you through the process of deploying a web application using Docker Swarm on AWS. By the end of this tutorial, you will have a robust and scalable setup for your web app.

### **✅ Solving the Problem 🧩**

By deploying your web app using Docker Swarm on AWS, you are addressing several key challenges:

* **Scalability**: Docker Swarm enables you to scale your application horizontally by adding or removing nodes seamlessly. This ensures your app can handle increased traffic.
    
* **High Availability**: With Swarm, your app is distributed across multiple nodes, making it highly available. If one node fails, the others can continue serving the application.
    
* **Simplified Management**: Docker Swarm provides an easy-to-use interface for managing containerized applications, reducing the complexity of orchestration.
    
* **Resource Efficiency**: Containers consume fewer resources compared to traditional virtual machines, optimizing resource utilization and reducing costs.
    

### **✅ Step 1: Provision AWS Instances 🌐**

* Start by logging into your AWS portal and create three new EC2 instances, each with unique names:
    
    * Swarm-manager
        
    * Swarm-worker1
        
* Ensure that you configure the inbound rules for these instances to allow the following traffic:
    
    * Custom TCP port 2377 from anywhere (IPv4)
        
    * Custom TCP port 8001 from anywhere (IPv4)
        

### **✅ Step 2: Install Docker 🐳**

SSH into each of the two instances and install Docker with the Docker Engine. You can refer to Docker's official documentation or other resources for detailed instructions on Docker installation.

### **✅ Step 3: Initialize Swarm on Swarm Manager 🤖**

Access the "Swarm Manager" node and initiate the Swarm by running the following command:

```plaintext
sudo docker swarm init
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692707382103/e77a77ba-bfb2-44db-8761-6b279880dab6.png align="center")

This command initializes an empty Swarm.

### **✅ Step 4: Add Workers to the Swarm 🏗️**

After initializing the Swarm on the "swarm-manager" node, a key will be generated. You need to copy and run this key on the other two servers (Swarm-worker1). This step adds both machines as workers to the Swarm.

### **✅ Step 5: Check Swarm Node Status 🚥**

To verify the status of all nodes in the Swarm, run the following command on the manager node:

```plaintext
docker node ls
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692707416967/d1183a49-ba02-4787-b6a3-cbf8a8ba815d.png align="center")

This command will display information about all the nodes in the Swarm.

### **✅ Step 6: Create a Docker Service 🛠️**

On the Swarm Manager node, create a Docker service using the following command:

```plaintext
sudo docker service create --name django-app-service --replicas 2 --publish 8001:8001 trainwithshubham/react-django-app:latest
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692707608416/21ed3a08-06e4-4041-9953-76b6e34164fc.png align="center")

This command creates a service named "django-app-service" with three replicas, publishing port 8001.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692709149707/ec83c127-445b-4b98-aaa6-693152611149.png align="center")

### **✅ Step 7: List Docker Services 📋**

To list the Docker services running in the Swarm, use the following command:

```plaintext
sudo docker service ls
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692707636964/d309b04d-9000-44f7-ace0-d9b16308b3c3.png align="center")

This will display a list of services, including the one you just created.

### **✅ Step 8: Verify Containers 🐋**

The service you created will deploy containers on the manager and worker nodes. To check if containers are running on the manager node, execute:

```plaintext
sudo docker ps
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692707673523/b2d3839b-84ed-4c6d-98ae-d66055520472.png align="center")

You should see containers related to your service.

### **✅ Step 9: Access the Web App 🌐**

Now, your web app service is running on all three nodes. To access it, grab the IP address of any of the nodes followed by port 8001, like this:

```plaintext
http://<Any_IP_of_2_VMs>:8001
http:3.82.60.74:8001
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692707733823/ec99d285-454e-4356-8d64-4eaf9cbc71b6.png align="center")

You should be able to access your web application through this URL.

### **✅ Step 10: Removing Nodes ♻️**

If you need to remove a node from the Swarm environment, run the following command on the specific worker node:

```plaintext
sudo docker swarm leave
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692708698218/a8326175-ad62-4639-a796-b04f37dae109.png align="center")

As a result, the worker node will leave the Swarm, and you can confirm its status by checking the output of:

```plaintext
docker node ls
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692708732776/291a7d46-a14e-40ac-83e6-06746ca2f415.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692708821041/d266779e-9006-4caa-b70d-d83797fcc1c3.png align="center")

# **📍** Conclusion

Congratulations! 🎉 You've successfully deployed a production-ready web app using Docker Swarm on AWS. Docker Swarm's orchestration capabilities make it easier to manage and scale your application, ensuring it runs smoothly in a production environment. Feel free to connect and follow for more informative content on containerization and cloud computing.

### **🔍 Checkout GitHub Repository for projects:**

**🔗** [**github.com/sumanprasad007**](http://github.com/sumanprasad007)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692607442282/98c6c100-886d-4894-80bc-db5df0141100.png?auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

### **🔍 Check out my YouTube channel - Prasad Suman Mohan:**

🔗 [**youtube.com/@sumanprasad007**](http://youtube.com/@sumanprasad007)

%[https://youtu.be/oVJoN5Zc3Kw]