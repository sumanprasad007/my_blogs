---
title: "Mastering Ansible Variables and Facts: Unleashing the Power of Dynamic Automation 🌐🚀"
datePublished: Sat Nov 18 2023 11:56:09 GMT+0000 (Coordinated Universal Time)
cuid: clp3ztkjn000h09l4e9oz79w7
slug: mastering-ansible-variables-and-facts-unleashing-the-power-of-dynamic-automation
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1700308546225/9d14c2ca-9a14-43e1-bcc0-c157205a01b3.gif
tags: aws, ansible, devops, 90daysofdevops, trainwithshubham

---

## Introduction to Ansible Variables and Facts

In the realm of Ansible, flexibility is key. Variables and facts provide the dynamism required to make your automation truly adaptable. In this blog post, we'll delve into the world of Ansible Variables and Facts, learning how to work with them and seamlessly integrate them into your playbooks.

## Working with Variables and Facts

### Understanding Ansible Facts

In Ansible, facts are pieces of information about remote hosts. Ansible gathers facts automatically when a playbook is executed. You can use these facts to make your playbooks more dynamic.

### Displaying Facts

To see the facts gathered by Ansible, use the `ansible` command with the `-m setup` module:

```plaintext
ansible all -m setup
```

This command displays a plethora of information about each host.

## Using Variables in Playbooks

### Declaring Variables

In Ansible, variables can be defined at various levels: globally, in a playbook, or even in a specific task. Let's create a simple playbook that uses variables:

```plaintext
---
- name: Use Variables
  hosts: web_servers
  become: yes
  vars:
    nginx_port: 80
    nginx_version: "1.18.0"
  tasks:
    - name: Install Nginx
      apt:
        name: nginx
        state: present
    - name: Start Nginx
      service:
        name: nginx
        state: started
      vars:
        nginx_port: "{{ nginx_port }}"
```

In this example, we've declared two variables (`nginx_port` and `nginx_version`) globally in the playbook.

### Dynamic Variable Assignment

You can also dynamically assign variables based on facts. Let's modify our playbook to use the fact `ansible_distribution`:

```plaintext
---
- name: Use Dynamic Variables
  hosts: web_servers
  become: yes
  tasks:
    - name: Display OS Distribution
      debug:
        var: ansible_distribution
    - name: Install Nginx
      apt:
        name: nginx
        state: present
      vars:
        nginx_port: "{{ 80 if ansible_distribution == 'Ubuntu' else 8080 }}"
```

Here, we've dynamically assigned the `nginx_port` variable based on the OS distribution.

## Conclusion

Variables and facts in Ansible bring a new level of dynamism to your automation. Whether you're adapting to different environments or customizing configurations, mastering variables is essential.

In the next blog post, we'll explore more advanced topics, including conditionals and loops in Ansible Playbooks. Get ready to elevate your automation game! 🚀🔍