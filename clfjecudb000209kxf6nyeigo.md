---
title: "Ansible Zero to Hero"
datePublished: Wed Mar 22 2023 08:02:32 GMT+0000 (Coordinated Universal Time)
cuid: clfjecudb000209kxf6nyeigo
slug: ansible-zero-to-hero
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1679472118799/29d53ffa-c476-4c04-955a-63e850985ff2.jpeg
tags: aws, python, developer, devops, beginners

---

In this post, I would like to introduce you to Ansible which is a popular open-source automation tool used by DevOps engineers for managing configurations, deploying applications, and orchestrating complex tasks across a large number of servers. In this article, we'll explore Ansible and how it can be used to manage EC2 instances in AWS.

# **📍** Introduction to Ansible

Ansible is a powerful automation tool that allows DevOps engineers to manage their infrastructure as code. With Ansible, you can automate the deployment of applications, the configuration of servers, and the orchestration of complex tasks across a large number of servers. Ansible uses a simple and easy-to-learn YAML syntax for creating playbooks that define the tasks to be performed.

## **📢** Installation of Ansible on EC2 Instance, step by step

To install Ansible on an EC2 instance, follow these steps:

1. Launch an EC2 instance with Amazon Linux 2 as the operating system.
    
2. SSH into the instance.
    
3. Run the following commands to install Ansible:
    

```python
sudo yum update -y
sudo amazon-linux-extras install ansible2 -y
```

1. Verify the installation by running the following command:
    

```python
ansible --version
```

# **📍** Passwordless authentication to other EC2 Instances and its steps

When using Ansible to manage multiple EC2 instances, it's important to set up passwordless authentication to allow Ansible to access the other instances without requiring a password. There are two ways to achieve this: using ssh-copy-id or ssh key-gen.

## **📢** Using ssh-copy-id

To use ssh-copy-id, follow these steps:

1. Generate a key pair on the Ansible host:
    

```python
ssh-keygen
```

1. Copy the public key to the other EC2 instances:
    

```python
ssh-copy-id <user>@<ip>
```

1. Repeat step 2 for all other EC2 instances.
    

## **📢** Using ssh key-gen

To use ssh key-gen, follow these steps:

1. Generate a key pair on the Ansible host:
    

```python
ssh-keygen
```

1. Copy the public key to the other EC2 instances:
    

```python
cat ~/.ssh/id_rsa.pub | ssh <user>@<ip> 'cat >> ~/.ssh/authorized_keys'
```

1. Repeat step 2 for all other EC2 instances.
    

# **📍 Ansible Adhoc:**

What are Ansible ad-hoc commands used for?

Ansible ad-hoc commands are used when you need to execute one or two tasks on a remote host without creating a playbook. Ad-hoc commands are useful for tasks such as checking disk space or creating a file on a remote host.

The basic syntax for running an ad-hoc command is:

```python
ansible -i inventory <target> -m "<module>" -a "<arguments>"
```

For example, the following command creates a file named "sample.txt" on all hosts in the inventory file:

```python
ansible -i inventory all -m "shell" -a "touch sample.txt"
```

What's the need to do grouping in the inventory file or how we can perform a certain task only on specific servers

When you want to run a playbook on specific hosts or groups of hosts, you can use inventory files to group them. Inventory files allow you to group hosts by their roles, environments, or any other criteria that you choose. This makes it easier to manage large infrastructures and run specific tasks on specific servers.

For example, you might want to run a playbook only on a group of database servers. You can define this group in your inventory file like this:

One of the key features of Ansible is its ability to group servers in the inventory file. Grouping servers allows you to perform specific tasks on specific servers. For example, you can group servers based on their function, such as web servers, database servers, or application servers. This enables you to run playbooks on specific groups of servers, rather than on all servers in the inventory.

# **📍 Ansible Playbook:**

An Ansible playbook is a set of instructions or tasks that can be executed on one or more servers. It is similar to a shell script file, but with additional capabilities that make it more powerful and flexible. Playbooks are written in YAML format, which is easy to read and understand.

Let's take an example of installing and starting the NGINX server on a target server. We can write a playbook to perform this task as follows:

```python
---
- name: Install and Start NGINX Server
  hosts: all
  become: true

  tasks: 
    - name: Install nginx
      apt:
        name: nginx
        state: present
        
    - name: Start nginx
      service:
        name: nginx
        state: started
```

Here, we have defined a playbook that installs the NGINX server on all hosts in the inventory file and starts the NGINX service. The `hosts` parameter specifies the group of servers on which the playbook will be executed. The `become` parameter specifies that the following commands will be executed as the root user.

## **📢** To run this playbook,

we can use the following command:

```python
ansible-playbook -i inventory-file first-playbook.yml
```

In case you want to debug and understand the commands running using the playbook, you can use the Verbosity (-v, -vv, or -vvv) option with the ansible-playbook command. For example:

```python
ansible-playbook -vvv -i inventory-file first-playbook.yml
```

One of the real-time examples of using Ansible in DevOps is the configuration of Kubernetes cluster. You can use Ansible to configure a Kubernetes master node and worker nodes. You can also create Ansible roles, which is an efficient way of writing Ansible playbooks. It provides readability, reduces the chance of making mistakes, and helps to manage secrets and multiple Ansible tasks easily.

## **📢**To create an Ansible role,

you can use the following command:

```python
ansible-galaxy role init kubernetes
```

This will create a Kubernetes folder with all the necessary Ansible role files

# **📍 Conclusion:**

I hope this post helps you to understand the basics of Ansible and how it can be used in DevOps. Please refer to the documentation to get the latest and updated commands and instructions. Let me know your thoughts in the comments. Ansible is a powerful and flexible automation tool that can help IT teams automate repetitive tasks, reduce the time and effort required for managing infrastructure, and achieve DevOps goals. By grouping servers in the inventory file, you can perform specific tasks on specific servers. Playbooks are used to write a set of multiple commands to perform on the server. Ansible roles provide an efficient way of writing Ansible playbooks and help manage secrets and multiple Ansible tasks easily.

# **📍 Resources:**

> ***YT Video:*** [https://youtu.be/Z6T2r3Xhk5k?list=PLdpzxOOAlwvIKMhk8WhzN1pYoJ1YU8Csa](https://youtu.be/Z6T2r3Xhk5k?list=PLdpzxOOAlwvIKMhk8WhzN1pYoJ1YU8Csa)

```python
I invite you to check my portfolio in case you are interested in contacting me for a project!. Prasad Suman Mohan

🔵 Don't forget to follow me also on LinkedIn: https://www.linkedin.com/in/prasad-suman-mohan/
```

%[https://youtu.be/Z6T2r3Xhk5k?list=PLdpzxOOAlwvIKMhk8WhzN1pYoJ1YU8Csa]