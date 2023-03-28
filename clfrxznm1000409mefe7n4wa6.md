---
title: "Configuring Load Balancer Using Ansible Playbook"
datePublished: Tue Mar 28 2023 07:34:18 GMT+0000 (Coordinated Universal Time)
cuid: clfrxznm1000409mefe7n4wa6
slug: configuring-load-balancer-using-ansible-playbook
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1679988689572/2f8b246c-b3c6-49ef-8981-7bc673fc080c.jpeg
tags: linux, python, developer, devops, beginners

---

# **📍 Introduction:**

In today's world, with the increasing number of users accessing applications, it has become essential to ensure that the application's load is distributed efficiently across multiple servers. This is where load balancers come into play. Load balancers help in distributing traffic between multiple servers, which not only helps in improving the reliability of the application but also aids in scaling it up. In this blog post, we will explore how to use Ansible to configure and manage load balancers, such as HAProxy.

## **🔹 Step 1: Installing Ansible**

Before we start configuring our load balancer, we need to install Ansible. Ansible can be installed on any Linux distribution, and it requires Python 2.7 or Python 3.5 or later.

To install Ansible on Ubuntu, run the following command:

```python
sudo apt update
sudo apt install ansible
```

## **🔹 Step 2: Configuring HAProxy**

HAProxy is an open-source load balancer that can be used to distribute traffic between multiple servers. To configure HAProxy using Ansible, we need to create an Ansible playbook that defines the desired state of our load balancer.

```python
---
- name: Install and configure HAProxy
  hosts: loadbalancer
  become: yes
  tasks:
    - name: Install HAProxy
      apt:
        name: haproxy
        state: present
    - name: Configure HAProxy
      template:
        src: templates/haproxy.cfg.j2
        dest: /etc/haproxy/haproxy.cfg
      notify:
        - restart haproxy
  handlers:
    - name: restart haproxy
      service:
        name: haproxy
        state: restarted
```

In this playbook, we first install HAProxy using the `apt` module. We then configure HAProxy by using a Jinja2 template to generate the `haproxy.cfg` configuration file. Finally, we define a handler to restart the HAProxy service when the configuration file changes.

## **🔹 Configuration file:**

The template file `haproxy.cfg.j2` contains the configuration for our load balancer. Here is an example configuration that distributes traffic between two servers:

```python
global
  log /dev/log local0
  log /dev/log local1 notice
  chroot /var/lib/haproxy
  user haproxy
  group haproxy
  daemon

defaults
  log global
  mode http
  option httplog
  option dontlognull
  timeout connect 5000
  timeout client 50000
  timeout server 50000

frontend http_front
  bind *:80
  default_backend http_back

backend http_back
  balance roundrobin
  server web1 192.168.0.101:80 check
  server web2 192.168.0.102:80 check
```

In this configuration file, we define a frontend that listens on port 80 and forwards traffic to a backend that distributes traffic between two servers with IP addresses 192.168.0.101 and 192.168.0.102.

## **🔹 Step 3: Running the playbook**

After creating our playbook and configuration files, we can run the playbook using the `ansible-playbook` command:

```python
ansible-playbook -i inventory.ini haproxy.yml
```

In this command, `-i inventory.ini` specifies the inventory file that contains the IP addresses of our load balancer, and `haproxy.yml` is the name of our playbook file.

After executing this command, Ansible will configure HAProxy on our load balancer, and traffic will be distributed between the two servers specified in our configuration file.

# **📍 Conclusion:**

Load balancers have become a crucial component for efficient application delivery. Load balancers distribute traffic across multiple servers, improving reliability and scalability. With Ansible, we can easily configure and manage load balancers like HAProxy or Nginx. In this blog post, we learned how to use Ansible to configure HAProxy by creating an Ansible playbook that defines the desired state of our load balancer. We also explored the configuration file for HAProxy and how to run the playbook to configure the load balancer. By using Ansible, we can automate the process of configuring and managing load balancers, saving time and improving efficiency in application delivery.

### *⚜ Follow Prasad Suman Mohan for many such contents:*

> * *LinkedIn:* [***linkedin.com/in/prasad-suman-mohan***](http://linkedin.com/in/prasad-suman-mohan)
>     
> * *Blog:* [***sumanprasad.hashnode.dev***](http://sumanprasad.hashnode.dev)
>