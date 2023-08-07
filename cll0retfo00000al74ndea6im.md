---
title: "Hosting a Two-Tier Flask Application with MySQL Database Using Docker Compose 👨‍💻🐳"
datePublished: Mon Aug 07 2023 10:58:36 GMT+0000 (Coordinated Universal Time)
cuid: cll0retfo00000al74ndea6im
slug: hosting-a-two-tier-flask-application-with-mysql-database-using-docker-compose
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1691405509390/62648759-668f-481e-abd0-8e2932a2a75f.png
tags: linux, python, developer, devops, 90daysofdevops

---

# **📍** Introduction:

In this tutorial, we will guide you through the process of hosting a two-tier Flask application with a MySQL database using Docker Compose. This architecture allows you to separate your frontend (Flask application) from your backend (MySQL database) and deploy them together using containers. We assume you have a basic understanding of Git, Docker, and Python. Let's get started! 🚀

### **🔍Prerequisites 🛠️**

Before we dive in, make sure you have the following prerequisites in place:

* Basic understanding of Git, Docker, and Python.
    
* Open port 5000 from your inbound rule (security group) of the server
    
* Docker is installed and running on your system. You should also be added to the Docker group to execute Docker commands without `sudo`.
    
* Internet connectivity to clone the GitHub repository and download Docker images.
    

### **Step 1: Clone the Repository 📂**

Let's start by cloning the repository containing the source code for our two-tier application. Open your terminal and execute the following commands:

```plaintext
git clone https://github.com/sumanprasad007/two-tier-flask-app.git

cd two-tier-architecture-flask-application-with-mysql-database
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691405592706/7a3b178d-44e3-4471-943a-e7ada171f313.png align="center")

You're now ready to dive into the project!

### **Step 2: Install Docker Compose 🐋**

If you haven't already installed Docker Compose, no worries! Run this command to install it:

```plaintext
sudo apt install docker-compose -y
```

Docker Compose will help us manage our multi-container application effortlessly.

### **Step 3: Start the Application with Docker Compose 🚢**

Now, let's use Docker Compose to start our two-tier application. Execute this command in the terminal:

```plaintext
docker-compose up -d
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691405618385/3f3a0b72-36f3-43f4-89a1-95be2b4d04a9.png align="center")

This command will create and start the containers defined in the `docker-compose.yml` file in detached mode. Smooth sailing ahead! ⛵

### **Step 4: Verify Containers 🕵️‍♂️**

To make sure everything is up and running, execute the following command:

```plaintext
docker ps
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691405677056/0347fd28-d0eb-4fef-9379-652ad3cb90a1.png align="center")

This will display a list of running containers. Keep an eye out for any issues!

### **Step 5: Create a MySQL Data Volume 🗄️**

Now, let's create a data volume to store the MySQL data. Run this command:

```plaintext
sudo mkdir /var/lib/mysql/
```

Our data will be securely stored and ready for action.

### **Step 6: Access MySQL Database 💾**

Time to dive into the MySQL database running in the container. First, find the container name using the `docker ps` command. Then, use the following command to access the MySQL shell:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691405738133/25d09225-df9e-4bd7-bf19-2d9b159d0dab.png align="center")

```plaintext
docker exec -it CONTAINER_NAME bash 

mysql -u root -p
```

### **Step 7: Creating table messages along with column**

You'll need to enter the MySQL root password. Once logged in, execute these SQL commands to interact with the database:

```plaintext
use two_tier;

show tables;

create table messages (message varchar(255));

describe messages;
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691405773287/5ec52776-5219-47e9-a7f9-1191171bc60d.png align="center")

You're now in control of your database schema!

### **Step 8: Access the Application 🌐**

To witness your Flask application in action, open a web browser and enter the following URL:

```plaintext
http://PUBLIC_IP_OF_SERVER:5000
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691405808004/5d7530f9-6df0-4364-b58b-8979fb23de88.png align="center")

Replace `PUBLIC_IP_OF_SERVER` with the actual public IP address of your server. Enjoy the view of your hard work!

## **Conclusion 🎉**

Congratulations! You've successfully hosted a two-tier Flask application with a MySQL database using Docker Compose. 🎈 This architecture gives you the power to manage your application components as isolated containers, ensuring scalability and maintainability. Remember, this tutorial provides a basic setup. In a production environment, consider additional factors like security, data backup, and container orchestration.

Feel free to explore and modify the source code to build more advanced features on top of this foundation. Happy coding! 💻🌟

### **🔍 Checkout GitHub Repository for projects:**

**🔗** [**github.com/sumanprasad007**](http://github.com/sumanprasad007)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690656559825/0474ff76-1d75-4ce0-93ea-1194d2444f74.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

### **🔍 Check out my YouTube channel - Prasad Suman Mohan:**

🔗 [**youtube.com/@sumanprasad007**](http://youtube.com/@sumanprasad007)

[![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690893614276/e567a0e4-c76d-4f49-b537-34ca8e727e5d.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")](https://www.youtube.com/@sumanprasad007)