---
title: "Mastering Infrastructure Automation with Ansible: A Comprehensive Guide"
datePublished: Thu Mar 23 2023 05:58:12 GMT+0000 (Coordinated Universal Time)
cuid: clfkpctes000a09kz7ctl1gzg
slug: mastering-infrastructure-automation-with-ansible-a-comprehensive-guide
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1679550798718/30d43f9b-9792-41ac-a16e-2727a8650ab3.png
tags: aws, python, developer, devops, beginners

---

# **📍 Introduction:**

In this blog, we'll cover the basics of configuration management and explore the benefits of using Ansible as a configuration management tool. We'll also take a closer look at Ansible's dynamic inventory, Galaxy commands, and roles.

1. ## What's Configuration Management?
    

Configuration management is a process used to manage infrastructure, system and keep our servers up to date. It involves managing configurations across multiple servers, installing security patches, and installing any dependencies on all of them at once. It helps to ensure that servers are configured consistently and can reduce the risk of configuration drift.

1. ## Is Ansible Better Than Other Configuration Management Tools?
    

Ansible is a popular configuration management tool that offers several benefits. Here are some of the reasons why Ansible stands out:

* Agentless: Ansible only needs passwordless authentication, making it easy to use without installing any software on the servers you're managing.
    
* Great community: Ansible is based on Python, which means it has a large and active community that can offer support and contribute to its development.
    
* Push mechanism: Ansible uses a push mechanism, which allows you to make changes quickly and easily.
    
* Cross-platform support: Ansible is compatible with both Windows and Linux servers.
    
* Easy to write playbooks: Ansible playbooks are written in YAML, which is a key-value pairs-based language that's easy to learn and read.
    

1. ## Writing an Ansible Playbook to Install and Run Httpd Service
    

Here's an example playbook to install and run the httpd service on an Ubuntu server:

```python
---
- name:
  become: root
  
  tasks:
    - name: Installing Httpd server
      commands:
        apt:
          state: present
    - name: Running Httpd server
      commands:
        apt:
          state: started
```

(Note: This playbook is for Ubuntu OS.)

1. ## How Ansible Can Help Your Organization?
    

Ansible can help your organization in many ways, such as:

* Managing test servers: Ansible can help manage test servers by installing, updating, and managing multiple Ubuntu servers, making it easier to perform PoCs.
    
* Automation: Ansible can automate tasks, reducing the risk of errors and freeing up time for other tasks.
    

1. ## What's Ansible Dynamic Inventory?
    

Ansible dynamic inventory is a feature that allows Ansible to automatically detect and configure servers without human intervention. For example, if you add new instances to your AWS account, Ansible will automatically configure the new servers.

1. ## What's Ansible Tower and Where You Used It?
    

Ansible Tower is a GUI model of Ansible that's designed to help beginners understand how Ansible works. We can use it to manage our Ansible environment and automate workflows.

1. ## How Do You Manage RBAC of Users on Ansible Tower?
    

Ansible Tower uses role-based access control (RBAC) to group users based on their roles and permissions. For example, you can create a group of users who have read-only access to a specific playbook or task. For AWS, you can integrate Ansible Tower with IAM.

1. ## What's Ansible Galaxy Commands, and Why Is It Used?
    

Ansible Galaxy is a tool used to create a whole structure for the playbook and manage secrets and multiple Ansible tasks easily.

1. ## Ansible Playbook using roles:
    

In Ansible, a role is a pre-defined way of organizing tasks, handlers, files, templates, and variables in a specific way. It's like a collection of tasks that perform a specific function or set of functions. We can create a role in Ansible using the ansible-galaxy command.

A role consists of the following directories:

* tasks: This directory contains all the tasks that need to be performed in the playbook.
    
* handlers: This directory contains all the handlers that are used by the playbook.
    
* files: This directory contains all the files that need to be transferred to the remote hosts.
    
* templates: This directory contains all the templates that are used by the playbook.
    
* vars: This directory contains all the variables that are used by the playbook.
    
* meta: This directory contains all the metadata that describes the role.
    
* defaults: This directory contains all the default values for the variables that are used by the playbook.
    

Using roles makes it easy to organize tasks and makes the playbook more modular and reusable.

1. ## Handlers in Ansible:
    

Handlers are like tasks in Ansible, but they are only triggered when a task contains a notify directive. A handler is used to start or stop a service, restart a service, or reload a configuration file after a change has been made.

Handlers are defined in the handlers directory of the role. The syntax for defining a handler is similar to defining a task, but the name of the handler should start with "handler\_". For example:

* name: Restart Apache service: name: apache2 state: restarted become: true when: apache\_changed
    
* name: Reload Configuration service: name: apache2 state: reloaded become: true when: apache\_changed
    

Here, we have defined two handlers, one to restart the Apache service and another to reload the configuration file. These handlers will be triggered when a task in the playbook has the notify directive.

1. ## Running specific tasks on specific hosts:
    

We can use tags or environment variables to run specific tasks on specific hosts. We can define tags for a task using the "tags" parameter. For example:

---

* name: Install Apache apt: name: apache2 state: present become: true tags: apache
    

Here, we have defined a tag "apache" for the task "Install Apache". To run this task on specific hosts, we can use the "--limit" option with the tag name. For example:

ansible-playbook playbook.yml --limit webserver --tags apache

This command will run the "Install Apache" task only on the "webserver" host.

1. ## Parallel Execution in Ansible:
    

Yes, Ansible supports parallel execution. When we run a playbook on multiple hosts, Ansible runs the first task on all hosts, and then moves to the second task once the first task has completed on all hosts.

To run multiple tasks in parallel, we can create multiple playbooks and run them simultaneously. We can also use the "async" and "poll" parameters with a task to run it in the background and wait for it to complete.

1. ## Connecting to Windows VMs:
    

Ansible uses the WinRM (Windows Remote Management) protocol to connect to Windows VMs. WinRM is a SOAP-based protocol that allows remote management of Windows computers.

To connect to a Windows VM, we need to enable WinRM on the remote host and configure Ansible to use WinRM for the connection. We also need to specify the username and password or SSH key to use for authentication.

1. ## Precedence of playbook group\_vars, role\_vars, and extra\_vars:
    

In addition to the provided order, the precedence for variables in Ansible is as follows:

1. Command line arguments (`--extra-vars`)
    
2. Block variables (`vars` in a block)
    
3. Task variables (`vars` in a task)
    
4. Include variables (`vars` in an include statement)
    
5. Role defaults (`roles/role_name/defaults/main.yml`)
    
6. Inventory variables (in `host_vars/` or `group_vars/` directory)
    
7. Playbook variables (`vars` at the playbook level)
    
8. Role variables (`roles/role_name/vars/main.yml`)
    
9. Extra variables (`extra_vars` in a playbook or inventory file)
    

The variables at the top of the list take precedence over those at the bottom.

1. ## How do you handle secrets in Ansible?
    

Ansible provides the concept of "vaults" to handle secrets. A vault is a secure way of storing sensitive data, such as passwords, API keys, and other credentials, and can be used to encrypt files containing sensitive information. Ansible encrypts the data in the vault using an encryption key, which can be stored in a separate file or generated on the fly.

To use a vault in an Ansible playbook, the sensitive data can be stored in a separate YAML file and encrypted using the `ansible-vault` command. The encrypted file can then be added to the playbook and accessed using the `vault` command, which prompts the user for the vault password.

1. ## Can you use Ansible for IaC? Yes then compare it with Terraform.
    

Yes, Ansible can be used for Infrastructure as Code (IaC) to automate the deployment and configuration of infrastructure resources. Ansible uses a declarative approach to configuration management, where users describe the desired state of their infrastructure resources, and Ansible ensures that the current state matches the desired state.

However, Ansible is primarily focused on configuration management and orchestration, while Terraform is designed specifically for infrastructure provisioning and management. Terraform provides a more comprehensive set of features for IaC, including the ability to provision and manage resources across multiple cloud providers and on-premises infrastructure.

Additionally, Terraform has a built-in state management system that tracks the state of resources and ensures that the current state matches the desired state, providing greater consistency and predictability in infrastructure management.

1. ## Can you talk about the Ansible playbook you wrote for your organization and walk us through it?
    

Sure, I wrote an Ansible playbook to configure a Microsoft SQL Server on a Windows server. The playbook contains the following tasks:

1. Install the SQL Server prerequisites
    
2. Install SQL Server
    
3. Configure the SQL Server service account
    
4. Create a SQL Server database
    
5. Create a SQL Server login
    
6. Configure a SQL Server backup job
    

Each task is defined in a separate YAML file and organized into roles. The playbook uses variables to define the necessary information, such as the SQL Server version, instance name, database name, and backup schedule.

The playbook is run using the `ansible-playbook` command and can be easily customized to configure SQL Server on different Windows servers.

1. ## What do you think Ansible can improve?
    

While Ansible is a powerful tool for configuration management and orchestration, there is always room for improvement. Some areas where Ansible could be improved include:

* Complex verbosity: Currently, Ansible does not provide a good way to debug complex tasks and playbooks, making it difficult to troubleshoot issues.
    
* Windows support: Ansible's support for Windows could be improved, particularly for .NET applications that are primarily deployed on Windows servers.
    
* IDE support: Ansible could benefit from better integration with popular IDEs, including smart suggestions and auto-completion of commands. This could be
    

# **📍** Conclusion:

In conclusion, Ansible is a powerful tool for managing infrastructure automation and has several benefits, including being agentless, having a large community, and supporting both Windows and Linux servers. Ansible Playbooks and Roles make it easy to automate tasks such as installing and running services. Ansible Tower provides a user-friendly interface for managing Ansible configurations, while dynamic inventory enables automatic configuration of new instances. While there is room for improvement in some areas, such as better support for Windows and improved IDE plugins, Ansible remains a top choice for infrastructure automation.

# **📍 Resources:**

> [***YT Video:*** https://youtu.be/j5PgN0J3d7M](https://youtu.be/j5PgN0J3d7M)

%[https://youtu.be/j5PgN0J3d7M]