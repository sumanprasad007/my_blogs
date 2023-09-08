---
title: "Exploring Web Server Configurations for Different Use Cases 🌐"
datePublished: Fri Sep 08 2023 13:33:44 GMT+0000 (Coordinated Universal Time)
cuid: clman1kzu000909l62wpz7sh9
slug: exploring-web-server-configurations-for-different-use-cases
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1694179868269/97a9f0a4-695f-424b-ab55-8a9611797c5d.png
tags: aws, web-development, developer, devops, 90daysofdevops

---

## 📍**Introduction:**

In the world of web hosting and applications, the choice of a web server plays a crucial role in determining the performance, security, and accessibility of your online presence. Let's dive into the setup of three popular web servers—nginx, HAProxy, and Apache 2—each tailored to distinct use cases. 🚀

![Ejecutar Apache Nginx y HAProxy en el mismo servidor ubuntu 20.04 -  Tecnolitas](https://tecnolitas.com/wp-content/uploads/2021/12/image.png align="left")

### **Nginx - Restricting Access Using nginx.conf** 🚧

*Use Case:* Control Access to Sensitive Areas

**Steps:**

1. 📝 Open your nginx configuration file at `/etc/nginx/nginx.conf`.
    
2. 📝 Within the `server` block, add a `location` block for the restricted area:
    
    ```plaintext
    server {
        listen 80;
        server_name yourdomain.com;
    
        location /restricted {
            deny all;
            return 403;
        }
    
        # ... other configuration ...
    }
    ```
    
3. 💾 Save the configuration file and restart nginx:
    
    ```plaintext
    sudo systemctl restart nginx
    ```
    
4. 🌐 Accessing `/restricted` will now yield a 403 Forbidden error.
    

![Apache vs Nginx: Melihat Perbedaannya Secara Mendalam](https://idwebhost.com/blog/wp-content/uploads/2020/05/IDwebhost-1024x600-1-1-scaled.jpg align="left")

### **HAProxy - Software Load Balancing & SSL Certificates** ⚖️🔐

*Use Case:* Load Balancing and SSL Termination

**Steps:**

1. 📝 Install HAProxy using:
    
    ```plaintext
    sudo apt-get install haproxy
    ```
    
2. 📝 Edit your HAProxy configuration file at `/etc/haproxy/haproxy.cfg`.
    
3. 📝 Configure the frontend for SSL termination:
    
    ```plaintext
    frontend https_frontend
        bind *:443 ssl crt /etc/haproxy/ssl/your_certificate.pem
        mode http
        option httplog
        default_backend backend_servers
    ```
    
4. 📝 Define the backend servers:
    
    ```plaintext
    backend backend_servers
        mode http
        balance roundrobin
        server webserver1 192.168.1.10:80
        server webserver2 192.168.1.11:80
        # Add more servers as needed
    ```
    
5. 💾 Save the configuration and restart HAProxy:
    
    ```plaintext
    sudo systemctl restart haproxy
    ```
    

### **Apache 2 - Setting Up a Web Server** 🛠️

*Use Case:* Basic Web Hosting

**Steps:**

1. 📝 Install Apache 2 with:
    
    ```plaintext
    sudo apt-get install apache2
    ```
    
2. 📝 Place your website files in `/var/www/html`.
    
3. 📝 Create a virtual host configuration:
    
    ```plaintext
    sudo nano /etc/apache2/sites-available/your_site.conf
    ```
    
    ```plaintext
    <VirtualHost *:80>
        ServerName yourdomain.com
        DocumentRoot /var/www/html/your_site
        # Other configuration directives
    </VirtualHost>
    ```
    
4. 📝 Enable the virtual host and necessary modules:
    
    ```plaintext
    sudo a2ensite your_site.conf
    sudo a2enmod rewrite
    ```
    
5. 📝 For SSL, use Let's Encrypt certificates with `certbot`:
    
    ```plaintext
    sudo apt-get install certbot python3-certbot-apache
    sudo certbot --apache
    ```
    
6. 💾 Restart Apache:
    
    ```plaintext
    sudo systemctl restart apache2
    ```
    

Choose the Right Web Server for Your Needs! 🛡️

## 📍 Conclusion:

Each web server discussed above has its strengths, making them suitable for different scenarios. Nginx excels at access control, HAProxy shines as a load balancer and SSL terminator, and Apache 2 offers a robust foundation for general web hosting. Tailor your choice to your project's unique requirements and enjoy a seamlessly running web application. 🚀🌐.

### **🔍 Checkout GitHub Repository for projects:**

**🔗** [https://linktr.ee/sumanprasad007](https://linktr.ee/sumanprasad007)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692607442282/98c6c100-886d-4894-80bc-db5df0141100.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

### **🔍 Check out my YouTube channel - Prasad Suman Mohan:**

🔗 [**youtube.com/@sumanprasad007**](http://youtube.com/@sumanprasad007)

%[https://youtu.be/oVJoN5Zc3Kw]