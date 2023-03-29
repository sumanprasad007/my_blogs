---
title: "Setup Nginx using Ansible Playbook"
datePublished: Wed Mar 29 2023 04:54:29 GMT+0000 (Coordinated Universal Time)
cuid: clft7pz7m000c09l9b87k2izu
slug: setup-nginx-using-ansible-playbook
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1679989856169/228f39ed-6dd5-4407-8bd0-c1da358142fa.png
tags: linux, python, developer, devops, beginners

---

# **📍 Introduction:**

Nginx is an open-source load balancer that can be used to distribute traffic between multiple servers. To configure Nginx using Ansible, we need to create an Ansible playbook that defines the desired state of our load balancer.

## **🔹 Step 1: Configuring Nginx**

Nginx is another open-source load balancer that can be used to distribute traffic between multiple servers. To configure Nginx using Ansible, we need to create an Ansible playbook that defines the desired state of our load balancer.

```python
---
- name: Install and configure Nginx
  hosts: loadbalancer
  become: yes
  tasks:
    - name: Install Nginx
      apt:
        name: nginx
        state: present
    - name: Configure Nginx
      template:
        src: templates/nginx.conf.j2
        dest: /etc/nginx/nginx.conf
      notify:
        - restart nginx
  handlers:
    - name: restart nginx
      service:
        name: nginx
        state: restarted
```

In this playbook, we first install Nginx using the `apt` module. We then configure Nginx by using a Jinja2 template to generate the `nginx.conf` configuration file. Finally, we define a handler to restart the Nginx service when the configuration file changes.

## **🔹 Step 2: Configuration file**

The template file `nginx.conf.j2` contains the configuration for our load balancer. Here is an example configuration that distributes traffic between two servers:

```python
worker_processes auto;
error_log /var/log/nginx/error.log;
pid /run/nginx.pid;

events {
    worker_connections 1024;
}

http {
    upstream backend {
        server 192.168.0.101:80;
        server 192.168.0.102:80;
    }

    server {
        listen 80;

        location / {
            proxy_pass http://backend;
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
        }
    }
}
```

In this configuration file, we define an upstream that contains two servers with IP addresses 192.168.0.101 and 192.168.0.102. We then define a server that listens on port 80 and forwards traffic to the upstream.

## **🔹 Step 3: Running the playbook**

After creating our playbook and configuration files, we can run the playbook using the `ansible-playbook` command:

```python
ansible-playbook -i inventory.ini nginx.yml
```

In this command, `-i inventory.ini` specifies the inventory file that contains the IP addresses of our load balancer, and `nginx.yml` is the name of our playbook file.

After executing this command, Ansible will configure Nginx on our load balancer, and traffic will be distributed between the two servers specified in our configuration file.

# **📍 Conclusion:**

In this blog post, we explored how to use Ansible to configure and manage load balancers, such as Nginx. Load balancers help in distributing traffic between multiple servers, which not only helps in improving the reliability of the application but also aids in scaling it up. We learned how to create an Ansible playbook that defines the desired state of our load balancer and how to run the playbook to configure our load balancer. By mastering Ansible, you can become a more efficient and effective system administrator and improve the reliability and scalability of your applications.

# **📍 Resources:**

> ***Image Credit:*** [](https://graspingtech.com/ansible-nginx-static-site/)[https://www.nginx.com/blog/announcing-nginx-core-collection-ansible/](https://www.nginx.com/blog/announcing-nginx-core-collection-ansible/)

```python
I invite you to check my portfolio in case you are interested in contacting me for a project!. Prasad Suman Mohan

🔵 Don't forget to follow me also on LinkedIn: https://www.linkedin.com/in/prasad-suma
```