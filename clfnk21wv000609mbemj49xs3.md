---
title: "Ansible Project - Automating Firewall Configuration"
datePublished: Sat Mar 25 2023 05:53:11 GMT+0000 (Coordinated Universal Time)
cuid: clfnk21wv000609mbemj49xs3
slug: ansible-project-automating-firewall-configuration
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1679723479663/9a7dccf4-4fd1-49c0-a2de-400e39688e07.jpeg
tags: aws, python, developer, devops, beginners

---

# **📍 Introduction:**

Securing your servers and restricting access to specific ports or IP addresses is an essential step in ensuring the safety of your infrastructure. One way to achieve this is by using firewall rules to control inbound and outbound traffic. However, configuring firewall rules on multiple servers can be a time-consuming and error-prone process. This is where Ansible comes in.

Ansible is an open-source automation tool that enables you to configure and manage multiple servers from a single control node. In this blog post, we will explore how to use Ansible to configure firewall rules on remote hosts.

## **🔹 Step 1: Install Ansible**

The first step in using Ansible to configure firewall rules is to install it on your control node. Ansible can be installed on various operating systems, including Linux, macOS, and Windows. For this blog post, we will be using Ubuntu 20.04 as our control node.

To install Ansible on Ubuntu 20.04, run the following command:

```python
sudo apt update
sudo apt install ansible
```

Once Ansible is installed, you can verify its version by running the following command:

```python
ansible --version
```

## **🔹 Step 2: Create an inventory file**

The next step is to create an inventory file that specifies the remote hosts you want to configure firewall rules on. The inventory file is a plain text file that contains the IP addresses or hostnames of your remote hosts. You can also group your hosts by using brackets \[\] and a group name.

For example, create a file named `hosts` in your current directory with the following contents:

```python
[web_servers]
192.168.1.10
192.168.1.11

[db_servers]
192.168.1.12
```

This file defines two groups: `web_servers` and `db_servers`. The `web_servers` group contains two hosts with IP addresses 192.168.1.10 and 192.168.1.11, while the `db_servers` group contains a single host with IP address 192.168.1.12.

## **🔹 Step 3: Create a playbook**

The next step is to create a playbook that defines the firewall rules you want to configure on your remote hosts. A playbook is a YAML file that specifies the tasks to be executed on your remote hosts.

For this blog post, we will create a playbook named `firewall.yml` that will configure firewall rules to allow inbound traffic on port 80 (HTTP) and port 443 (HTTPS) from any IP address. To achieve this, we will be using the `ufw` firewall tool that is available on Ubuntu and other Debian-based systems.

Create a file named `firewall.yml` in your current directory with the following contents:

```python
---
- name: Configure firewall rules
  hosts: all
  become: yes
  tasks:
  - name: Allow HTTP and HTTPS traffic
    ufw:
      rule: allow
      proto: tcp
      port: [80, 443]
```

This playbook defines a single task that allows inbound traffic on port 80 and port 443 using the `ufw` firewall tool. The `hosts: all` parameter specifies that the task should be executed on all hosts defined in the inventory file.

## **🔹 Step 4: Execute the playbook**

The final step is to execute the playbook on your remote hosts. To do this, run the following command from your control node:

```python
ansible-playbook -i hosts firewall.yml
```

This command executes the `firewall.yml` playbook on all hosts defined in the `hosts` inventory file.

After the playbook has finished executing, you can verify that the firewall rules have been applied by running the following command on your remote hosts:

```python
sudo ufw status
```

This command displays the status of the `ufw` firewall tool and should show that inbound traffic on port 80 and port 443 is now allowed.

## **🔹 Step 5: Restrict access to specific IP addresses**

In addition to allowing traffic on specific ports, you may also want to restrict access to specific IP addresses. This can be useful if you want to limit access to your servers to a specific set of clients.

To achieve this, you can modify the `firewall.yml` playbook to specify the allowed IP addresses using the `src` parameter of the `ufw` module. For example, the following playbook allows inbound traffic on port 22 (SSH) only from the IP address 192.168.1.100:

```python
---
- name: Configure firewall rules
  hosts: all
  become: yes
  tasks:
  - name: Allow SSH traffic from a specific IP address
    ufw:
      rule: allow
      proto: tcp
      port: 22
      src: 192.168.1.100
```

After executing this playbook, inbound traffic on port 22 will only be allowed from the IP address 192.168.1.100.

## **📍 Conclusion:**

In this blog post, we have seen how to use Ansible to configure firewall rules on remote hosts. By using Ansible, we can automate the process of configuring firewall rules and ensure that all servers are configured consistently. This can help to improve the security of our infrastructure and reduce the risk of unauthorized access.

We have also seen how to allow traffic on specific ports and restrict access to specific IP addresses. By combining these techniques, we can create a fine-grained security policy that meets the needs of our organization.

Ansible provides many other modules that can be used to automate the configuration of servers, including modules for managing packages, users, and services. By mastering Ansible, you can become a more efficient and effective system administrator and improve the security and reliability of your infrastructure.