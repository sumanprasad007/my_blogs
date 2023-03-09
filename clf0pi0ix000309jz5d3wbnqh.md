---
title: "Understanding - Server, Hypervisor, and Virtual Machines"
datePublished: Thu Mar 09 2023 06:06:51 GMT+0000 (Coordinated Universal Time)
cuid: clf0pi0ix000309jz5d3wbnqh
slug: understanding-server-hypervisor-and-virtual-machines
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1678341736204/d168c391-21c0-4193-af81-8459f5ee0881.jpeg
tags: tutorial, python, developer, devops, beginners

---

# **📍 Introduction using Illustrations:**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678341661322/f395811a-4974-4a35-bf0b-857ed4faf51b.png align="center")

Sam is the owner of a small IT company that provides various services to its clients. Sam had a limited budget for hardware, and he needed to find a way to run multiple applications on a limited number of physical machines.

He soon discovered the concept of virtual machines and hypervisors. He learned that virtual machines could create multiple operating systems on a single physical machine, allowing him to run multiple applications without purchasing additional hardware. Sam decided to implement virtual machines in his business. He chose a hypervisor that would manage and create multiple virtual machines on his physical server. He allocated hardware resources such as CPU, memory, and storage to each virtual machine as needed.

To give an example, Sam's company needed to run three different applications on three separate servers. Each application had its own set of hardware requirements, and each server had a different operating system requirement. Instead of purchasing three physical servers, Sam created three virtual machines on a single physical server, each with its own operating system and hardware resources allocated as needed.

With virtual machines, Sam was able to run multiple applications on a single physical machine, which resulted in significant cost savings. He no longer needed to purchase multiple physical servers, which meant lower hardware, energy, and maintenance costs. Sam was able to better manage and maintain his server infrastructure, as each virtual machine was isolated and could be managed separately. He also had the flexibility to easily add or remove virtual machines as his business needs changed.

In the end, Sam was happy with his decision to implement virtual machines and hypervisors. It allowed him to maximize the utilization of his physical resources while minimizing costs, and ultimately, helped his business grow and thrive.

# **📍 Defining Terminologies:**

## **🔹Server:**

A server is a computer program or device that provides services or resources to other computers or devices, known as clients, over a network. Servers can range from small home servers to large enterprise-level servers, and they can offer various types of services such as file storage, email, web hosting, database management, and more.

## **🔹Virtual Machine (VM):**

A virtual machine (VM) is a software-based emulation of a physical computer system that allows multiple operating systems to run on a single physical machine. It provides an isolated environment in which applications can run independently of the underlying hardware and operating system. The virtual machine emulates a set of hardware devices, including CPU, memory, storage, and network interfaces, which the guest operating system can use as if it were running on a physical machine.

## **🔹Hypervisor:**

A hypervisor, also known as a virtual machine manager, is a software layer that enables multiple virtual machines to run on a single physical machine. The hypervisor creates and manages the virtual machines, providing them with access to the physical resources of the host machine, such as CPU, memory, and storage.

The need for virtual machines arises from the desire to maximize the utilization of physical resources while minimizing costs. By creating multiple virtual machines on a single physical machine, it is possible to consolidate workloads and reduce the number of physical machines needed. This can result in significant savings in hardware, maintenance, and energy costs.

## **🔹Example:**

For example, suppose a company needs to run three different applications on three separate servers. Each server has a different operating system requirement, and each application has its own set of hardware requirements. Instead of purchasing three physical servers, the company can create three virtual machines on a single physical server, each with its own operating system and hardware resources allocated as needed. This results in lower hardware costs, reduced energy consumption, and easier management and maintenance of the server infrastructure.

# **📍 Conclusion:**

In conclusion, servers, virtual machines, and hypervisors are essential components in modern computing. Servers are programs or devices that provide resources or services to other devices over a network. Virtual machines are software-based emulations of physical computer systems that allow multiple operating systems to run on a single physical machine, while hypervisors are software layers that enable multiple virtual machines to run on a single physical machine. The need for virtual machines arises from the desire to maximize the utilization of physical resources while minimizing costs. By creating multiple virtual machines on a single physical machine, it is possible to consolidate workloads, reduce the number of physical machines needed, and ultimately save on hardware, maintenance, and energy costs. As illustrated in the example of Sam's IT company, the implementation of virtual machines and hypervisors can result in significant cost savings and provide a more flexible and manageable server infrastructure.