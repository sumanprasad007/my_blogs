---
title: "Ansible playbooks for DevOps Engineer Part -1"
datePublished: Fri Mar 24 2023 06:59:49 GMT+0000 (Coordinated Universal Time)
cuid: clfm6zwhy000409l90ftbg27i
slug: ansible-playbooks-for-devops-engineer-part-1
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1679640662536/765c2d0b-8217-4ce4-9532-9013db762f8d.png
tags: aws, python, developer, devops, beginners

---

# **📍 Introduction:**

In today's fast-paced world, managing multiple servers and ensuring their configuration can be a daunting task. It requires a significant amount of time and effort to manually install updates, set up software packages, and configure services on each server. However, with the use of automation tools like Ansible, we can simplify and streamline this process. Additionally, creating passwordless authentication using key-gen can make it easier to authenticate with remote servers without having to remember multiple passwords. In this scenario, we will learn how to create passwordless authentication and use Ansible playbooks to install updates, Git, AWS CLI, and set up Jenkins with the latest Java JDK. By implementing these steps, we can save time, reduce errors, and improve efficiency in managing our servers.

### **🔹**Here are the steps to create passwordless authentication using key-gen:

1. Open your terminal or command prompt.
    

1. Generate SSH keys using the ssh-keygen command on your Ansible control machine:
    

```python
Copy codessh-keygen
```

1. Copy the public key to all servers in the inventory:
    

```python
javascriptCopy codessh-copy-id -i ~/.ssh/id_rsa.pub <username>@<server_ip>
```

1. Verify that you can ssh to each server without being prompted for a password:
    

```python
phpCopy codessh <username>@<server_ip>
```

### **🔹**

### Next, let's create an inventory file to store 10 server IPs and group them as "ubuntu":

```python
[ubuntu]
server1_ip_address
server2_ip_address
server3_ip_address
...
server10_ip_address
```

Now, we will create the playbooks for installing updates, git, and aws cli as well as setting up Jenkins with the latest Java JDK.

### **🔹**Ansible playbook to install the latest updates and install git and AWS CLI:

```python
---
- name: Update and install packages
  hosts: ubuntu
  become: true
  tasks:
    - name: Update packages
      apt:
        update_cache: yes
        upgrade: dist
    - name: Install git
      apt:
        name: git
        state: present
    - name: Install AWS CLI
      apt:
        name: awscli
        state: present

     - name: Configure AWS CLI
      shell: aws configure set aws_access_key_id <your_access_key> && aws configure set aws_secret_access_key <your_secret_key>
      become_user: <remote_username>
```

### **🔹**Ansible playbook to install and setup Jenkins with the latest Java JDK:

```python
---
- name: Install and setup Jenkins
  hosts: ubuntu
  become: true
  tasks:
    - name: Install Java JDK
      apt:
        name: openjdk-11-jdk
        state: present
    - name: Add Jenkins repository key
      apt_key:
        url: https://pkg.jenkins.io/debian/jenkins.io.key
    - name: Add Jenkins repository to apt sources
      apt_repository:
        repo: deb https://pkg.jenkins.io/debian-stable binary/
        state: present
    - name: Install Jenkins
      apt:
        name: jenkins
        state: present
    - name: Start Jenkins service
      service:
        name: jenkins
        state: started
        enabled: true
```

# **📍 Conclusion:**

In this tutorial, we have learned how to create passwordless authentication using key-gen and how to use Ansible playbooks to install updates, git, aws cli, and set up Jenkins with the latest Java JDK. By following these steps, you can streamline your server configuration process and save time.

# **📍 Resources:**

> ***YT Video:*** [***https://youtu.be/Z6T2r3Xhk5k?list=PLdpzxOOAlwvIKMhk8WhzN1pYoJ1YU8Csa***](https://youtu.be/Z6T2r3Xhk5k?list=PLdpzxOOAlwvIKMhk8WhzN1pYoJ1YU8Csa)
> 
> Image Credit: [https://k21academy.com/devops-foundation/ansible-playbook-galaxy-tower/](https://k21academy.com/devops-foundation/ansible-playbook-galaxy-tower/)

```python
I invite you to check my portfolio in case you are interested in contacting me for a project!. Prasad Suman Mohan

🔵 Don't forget to follow me also on LinkedIn: https://www.linkedin.com/in/prasad-suma
```