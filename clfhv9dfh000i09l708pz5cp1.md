---
title: "Overview of Configuration Management Tool - Ansible"
datePublished: Tue Mar 21 2023 06:20:11 GMT+0000 (Coordinated Universal Time)
cuid: clfhv9dfh000i09l708pz5cp1
slug: overview-of-configuration-management-tool-ansible
tags: aws, python, developer, devops, beginners

---

# **📍 Introduction:**

Are you struggling with managing your infrastructure updates, security patches, and software installations? Configuration management is the solution you need to streamline and automate these tasks. In this blog, we will take a deep dive into the world of configuration management with a focus on Ansible.

## **📢** What's Configuration Management?

Configuration management is the practice of automating the process of managing and configuring servers, applications, and infrastructure. It ensures that your servers are up to date with the latest software patches, bug fixes, and security updates. Earlier, system admins used to write shell or PowerShell scripts to perform these tasks, but with the advent of cloud computing and microservices, the number of servers has increased significantly, making it challenging to manage these scripts.

To address this issue, several tools such as Puppet, Chef, Salt, and Ansible have been developed. Among these tools, Ansible is the most widely used and is managed by Red Hat.

## **📢** Why do we need to learn it?

Configuration management tools like Ansible can help you automate and streamline your infrastructure management tasks, save time and reduce errors. By learning Ansible, you can improve your efficiency and productivity as a DevOps engineer and manage your infrastructure more effectively.

## **📢** What are the basic terminologies associated with it?

Some of the basic terminologies associated with Ansible are inventory, playbooks, roles, modules, and tasks. The inventory is a list of hosts or servers that Ansible manages. A playbook is a set of instructions or tasks that Ansible performs on the hosts defined in the inventory. Roles are a collection of tasks and templates that can be reused across different playbooks. Modules are the building blocks of Ansible that perform individual tasks, such as copying a file or installing a package.

## **📢** Why did you pick Ansible over other tools like Puppet and Chef?

![](https://www.whizlabs.com/blog/wp-content/uploads/2020/01/Ansible_Vs_Puppet_Vs_Chef.png align="left")

Ansible offers several advantages over other configuration management tools like Puppet and Chef. Unlike Puppet, Ansible uses a push mechanism, where DevOps engineers write the script on their machine and push it to the servers to update. This eliminates the need for a master-slave architecture like Jenkins. Ansible also uses an agentless model, which means no master-slave/agent is required, and only the names of the servers (IP address or DNS) need to be provided in the inventory file.

Ansible is easier to use than Chef, as it uses a global language, YAML, that is popular and easy to learn. It also supports both Windows and Linux servers and offers up-to-date modules for both. Ansible is also dynamic and easy to scale up and down. It uses a new concept called Dynamic Inventory, which auto-detects changes, eliminating the need to update the configuration manually repeatedly. You can write your modules for your applications using Python and share them with others using Ansible Galaxy.

## **📢 Few Drawbacks:**

Disadvantages of Ansible include its poor performance when executing on large numbers of servers (10k servers and more) and its bit complex nature when managing complex Windows configurations. Additionally, Ansible's debugging capabilities could be improved.

# **📍** Some crucial questions regarding Ansible:

1. Which programming language is used to create modules in Ansible?
    
    Ans: Python is used to create modules in Ansible.
    
2. How compatible is Ansible with Windows and Linux?
    
    Ans: Ansible is compatible with both Windows and Linux servers.
    
3. Why do you prefer Ansible over other configuration management tools like Puppet and Chef?
    
    Ans: Ansible's push mechanism, passwordless authentication, and easy-to-use global language YAML make it easier to manage and scale up and down.
    
4. Is Ansible a push or pull mechanism, and can you explain them?
    
    Ans: Ansible is a push mechanism. The DevOps engineer writes the script in their machine and pushes it to the servers to update them.
    
5. What's YAML?
    
    Ans: YAML is a human-readable data serialization language commonly used for configuration files.
    
6. Is Ansible cloud-independent, and can you elaborate on your answer?
    
    Ans: Ansible is cloud-independent, meaning it can be used to manage infrastructure on any cloud platform or on-premises.
    
7. What's an Ansible playbook, and can you provide an example?
    
    Ans: An Ansible playbook is a set of instructions or tasks written in YAML format that is executed on a set of hosts
    

# **📍 Conclusion:**

Configuration management tools like Ansible can be a game-changer for infrastructure management. Ansible simplifies the process of managing servers, applications, and infrastructure by automating tasks and reducing errors. Its push mechanism, passwordless authentication, and easy-to-use global language YAML make it a preferred choice for DevOps engineers. Though it has some drawbacks, such as poor performance on large numbers of servers and complex Windows configurations, it remains one of the most widely used configuration management tools.

# **📍 Resources:**

> ***YT Video:*** [https://www.youtube.com/watch?v=I5\_NF8nvACg&list=PLdpzxOOAlwvIKMhk8WhzN1pYoJ1YU8Csa&index=17](https://www.youtube.com/watch?v=I5_NF8nvACg&list=PLdpzxOOAlwvIKMhk8WhzN1pYoJ1YU8Csa&index=17)
> 
> Blog Post: [https://www.whizlabs.com/blog/chef-vs-puppet-vs-ansible/](https://www.whizlabs.com/blog/chef-vs-puppet-vs-ansible/)

```python
I invite you to check my portfolio in case you are interested in contacting me for a project!. Prasad Suman Mohan

🔵 Don't forget to follow me also on LinkedIn: https://www.linkedin.com/in/prasad-suman-mohan/
```