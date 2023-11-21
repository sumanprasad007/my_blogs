---
title: "Ansible Playbook : Conditionals and Loops 🔄🚀"
datePublished: Tue Nov 21 2023 14:12:43 GMT+0000 (Coordinated Universal Time)
cuid: clp8f0ro9000009jubtq21mck
slug: ansible-playbook-conditionals-and-loops
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1700575915502/b8fab49e-2c65-4e05-b4cd-fce5155f6765.gif
tags: aws, web-development, ansible, devops, 90daysofdevops

---

## Introduction to Conditionals and Loops in Ansible Playbooks

In the intricate dance of automation, Ansible Playbooks are not just static scripts; they are dynamic orchestrations. Conditionals and loops add the magic touch, introducing flexibility and intelligence to your automation. In this blog post, we'll delve into the implementation of conditionals and loops in Ansible Playbooks, empowering your automation with decision-making and iterative capabilities.

## Implementing Conditionals in Ansible Playbooks

### Conditional Statements

Conditionals in Ansible are expressed through `when` statements. Let's consider a scenario where a task should only execute if a specific condition is met:

```plaintext
---
- name: Conditional Task
  hosts: web_servers
  become: yes
  tasks:
    - name: Ensure Nginx is installed (if Ubuntu)
      apt:
        name: nginx
        state: present
      when: ansible_distribution == 'Ubuntu'
```

In this example, the task will only execute on hosts where the distribution is Ubuntu.

### Conditional Blocks

For more complex scenarios, you can use conditional blocks:

```plaintext
---
- name: Conditional Block
  hosts: web_servers
  become: yes
  tasks:
    - name: Ensure Nginx is installed
      block:
        - name: Install Nginx (if Ubuntu)
          apt:
            name: nginx
            state: present
        - name: Install Nginx (if CentOS)
          yum:
            name: nginx
            state: present
      when: "'nginx' not in ansible_facts.packages"
```

This block installs Nginx based on the package's absence, regardless of the distribution.

## Embracing Loops in Ansible Playbooks

### Looping Through Items

Loops in Ansible allow you to iterate through a list of items. Consider a scenario where you want to create multiple users:

```plaintext
---
- name: Create Users
  hosts: web_servers
  become: yes
  vars:
    users_to_create:
      - alice
      - bob
      - charlie
  tasks:
    - name: Create Users
      user:
        name: "{{ item }}"
        state: present
      with_items: "{{ users_to_create }}"
```

This playbook creates users `alice`, `bob`, and `charlie`.

### Looping with `loop` Keyword

The `loop` keyword simplifies looping through a list:

```plaintext
---
- name: Create Users with loop
  hosts: web_servers
  become: yes
  vars:
    users_to_create:
      - alice
      - bob
      - charlie
  tasks:
    - name: Create Users
      user:
        name: "{{ item }}"
        state: present
      loop: "{{ users_to_create }}"
```

This accomplishes the same as the previous example.

## Conclusion

Conditionals and loops in Ansible Playbooks bring a dynamic dimension to your automation, allowing you to make decisions and iterate through tasks. As you incorporate these constructs into your playbooks, your automation becomes more adaptive and intelligent.

In the next blog post, we'll explore advanced topics, including dynamic inventories and best practices in Ansible. Get ready to take your automation game to new heights! 🚀🧠