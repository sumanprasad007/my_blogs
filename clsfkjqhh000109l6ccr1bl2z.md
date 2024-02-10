---
title: "Ansible Cheat Sheet with Real-Time Use Cases - Part 1🚀"
datePublished: Sat Feb 10 2024 04:20:57 GMT+0000 (Coordinated Universal Time)
cuid: clsfkjqhh000109l6ccr1bl2z
slug: ansible-cheat-sheet-with-real-time-use-cases-part-1
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1707504828594/f1bbd07a-256c-4917-9b08-b08a0556d6cb.png
tags: linux, docker, aws, python, web-development, ansible, kubernetes, webdev, developer, devops, 90daysofdevops, ansible-playbook, trainwithshubham, 90daysofdevops-chanllenge

---

## Introduction

Ansible is a powerful open-source automation tool that simplifies the configuration management, application deployment, and task automation processes. This cheat sheet provides a quick reference to commonly used Ansible commands and concepts, accompanied by real-time use cases to illustrate their practical application.

<div data-node-type="callout">
<div data-node-type="callout-emoji">💡</div>
<div data-node-type="callout-text">Download the Docker Cheat Sheet from below<strong> </strong><a target="_blank" rel="noopener noreferrer nofollow" href="https://www.linkedin.com/posts/prasad-suman-mohan_ansible-cheat-sheet-with-examples-part1-activity-7161936887811563520-L_Eo?utm_source=share&amp;utm_medium=member_desktop" style="pointer-events: none"><strong>link:</strong></a></div>
</div>

%[https://www.linkedin.com/posts/prasad-suman-mohan_ansible-cheat-sheet-with-examples-part1-activity-7161936887811563520-L_Eo?utm_source=share&utm_medium=member_desktop] 

## [Ansib](https://www.linkedin.com/posts/prasad-suman-mohan_docker-cheat-sheet-a-guide-for-devops-activity-7161206554610827264-4Z95?utm_source=share&utm_medium=member_desktop)le Cheat Sheet

### 1\. **Inventory Management**

* **Command:**`ansible-inventory`
    
* **Use Case:** List all hosts in the inventory.
    
* ```plaintext
      ansible-inventory --list
    ```
    

### 2\. **Ad-hoc Commands**

* **Command:**`ansible`
    
* **Use Case:** Run a command on all hosts in the inventory.
    
* ```plaintext
      ansible all -m command -a "uptime"
    ```
    

### 3\. **Playbooks**

* **Command:**`ansible-playbook`
    
* **Use Case:** Execute a playbook.
    
* ```plaintext
      ansible-playbook deploy-app.yaml
    ```
    

### 4\. **Variables**

* **Command:**`{{ variable_name }}`
    
* **Use Case:** Use a variable in a playbook.
    
* ```plaintext
      tasks:
        - name: Ensure package is installed
          apt:
            name: "{{ package_name }}"
            state: present
    ```
    

### 5\. **Loops**

* **Command:**`with_items`
    
* **Use Case:** Iterate over a list in a playbook.
    
* ```plaintext
      tasks:
        - name: Create users
          user:
            name: "{{ item }}"
            state: present
          with_items:
            - user1
            - user2
    ```
    

### 6\. **Conditionals**

* **Command:**`when`
    
* **Use Case:** Add a condition to a task.
    
* ```plaintext
      tasks:
        - name: Restart Apache if config file changes
          service:
            name: apache2
            state: restarted
          when: "'apache.conf' in ansible.builtin.changed_files"
    ```
    

### 7\. **Roles**

* **Command:**`ansible-galaxy`
    
* **Use Case:** Create a new role.
    
* ```plaintext
      ansible-galaxy init my-role
    ```
    

### 8\. **Vault**

* **Command:**`ansible-vault`
    
* **Use Case:** Encrypt sensitive data.
    
* ```plaintext
      ansible-vault encrypt secrets.yaml
    ```
    

### Real-Time Use Cases

1. **Deploying a Web Application:**
    
    * Use Ansible to deploy a web application on multiple servers, ensuring consistency and scalability.
        
2. **Configuring Monitoring Agents:**
    
    * Automate the installation and configuration of monitoring agents on servers using Ansible playbooks.
        
3. **Scaling Infrastructure:**
    
    * Dynamically scale your infrastructure by adding or removing servers based on demand using Ansible.
        
4. **Continuous Integration/Continuous Deployment (CI/CD):**
    
    * Integrate Ansible into your CI/CD pipeline to automate deployment tasks and ensure efficient release management.
        
5. **Database Configuration:**
    
    * Use Ansible to automate the setup and configuration of databases, ensuring a standardized environment.
        
6. **Security Patching:**
    
    * Implement Ansible to automate the process of applying security patches across multiple servers simultaneously.
        

### 9\. **Dynamic Inventory**

* **Command:**`ansible-inventory --graph`
    
* **Use Case:** Display the inventory structure in a graph.
    
* ```plaintext
      ansible-inventory --graph
    ```
    

### 10\. **Handlers**

* **Command:**`handlers`
    
* **Use Case:** Define a handler to restart a service only if a task triggers it.
    
* ```plaintext
      handlers:
        - name: restart apache
          service:
            name: apache2
            state: restarted
    ```
    

### 11\. **Tags**

* **Command:**`--tags` and `--skip-tags`
    
* **Use Case:** Run specific tasks or skip others based on tags.
    
* ```plaintext
      ansible-playbook deploy-app.yaml --tags "install,config"
    ```
    

### 12\. **Ansible Vault Encryption and Decryption**

* **Command:**`ansible-vault encrypt_string`
    
* **Use Case:** Encrypt sensitive strings for use in playbooks.
    
* ```plaintext
      ansible-vault encrypt_string 'secret_password' --name 'db_password'
    ```
    

### 13\. **Custom Modules**

* **Command:**`ansible-doc -l | grep your_module`
    
* **Use Case:** Develop and use custom Ansible modules.
    
* ```plaintext
      ansible-doc -l | grep custom_module
    ```
    

### 14\. **Jinja2 Templating**

* **Command:**`{{ variable | filter }}`
    
* **Use Case:** Use Jinja2 filters for dynamic content.
    
* ```plaintext
      tasks:
        - name: Set dynamic variable
          set_fact:
            dynamic_value: "{{ base_value | upper }}"
    ```
    

### 15\. **Notify and Wait for Completion**

* **Command:**`async` and `poll`
    
* **Use Case:** Execute tasks asynchronously and wait for their completion.
    
* ```plaintext
      tasks:
        - name: Long-running task
          command: /path/to/long_running_script.sh
          async: 300
          poll: 0
          register: job_result
      
        - name: Wait for completion
          async_status:
            jid: "{{ job_result.ansible_job_id }}"
          until: job_result.finished
          retries: 30
    ```
    

### Real-Time Use Cases (Continued)

1. **Automated Backup Strategy:**
    
    * Utilize Ansible to create an automated backup strategy, including regular backups and cleanup tasks.
        
2. **Multi-Environment Deployment:**
    
    * Manage deployments across multiple environments (e.g., development, staging, production) using dynamic inventories and environment-specific playbooks.
        
3. **Infrastructure Monitoring Setup:**
    
    * Automate the deployment of monitoring tools and configurations across servers to ensure real-time visibility into infrastructure health.
        
4. **Custom Module for Application-specific Tasks:**
    
    * Develop a custom Ansible module to handle application-specific tasks, providing flexibility in automation.
        
5. **Rolling Updates:**
    
    * Implement rolling updates for services, ensuring zero downtime during updates by using Ansible's serial and max\_fail\_percentage features.
        
6. **Git Repository Management:**
    
    * Automate tasks related to Git repositories, such as cloning, pulling updates, and managing branches.