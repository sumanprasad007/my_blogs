---
title: "Day 14: Security Groups: Guardians of Network Security 🌐🛡️"
datePublished: Wed Jan 03 2024 04:00:12 GMT+0000 (Coordinated Universal Time)
cuid: clqx92owe000008jobulj5kny
slug: day-14-security-groups-guardians-of-network-security
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1704214569770/8c8bfcd6-9359-4f76-9c60-09495a7d3311.gif
tags: linux, aws, technology, python, web-development, kubernetes, terraform, technical-writing-1, 90daysofdevops, trainwithshubham

---

## Unveiling Security Groups: Cornerstone of AWS Network Security 🔐🔍

### Core Functionality:

* **Definition:** Fundamental components governing network security in AWS.
    
* **Control:** Dictate the flow of traffic into and out of EC2 Instances.
    
* **Composition:** Solely comprised of rules, referencing IPs or other security groups.
    

## Security Groups in Action: A Closer Look 🧐🔒

### Acting as a Digital Firewall:

* **Role:** Serve as a virtual firewall for EC2 instances.
    
* **Regulation:**
    
    * Access to Ports.
        
    * Authorized IP ranges for both IPv4 and IPv6.
        
    * Control of inbound and outbound network traffic.
        

## Deep Dive into Security Groups: An Illustrated Overview 🚀🖼️

### Diagram: Understanding Traffic Filtering

* **Components:**
    
    * EC2 Instance.
        
    * Security Group 1.
        
    * Inbound and Outbound Rules.
        
    * Authorized and Unauthorized IPs.
        

## Key Insights about Security Groups: Essential Know-How 📚🌐

### Critical Points:

* **Versatility:** Attachable to multiple instances.
    
* **Scope:** Locked down to a specific region and Virtual Private Cloud (VPC) combination.
    
* **Location:** Operate outside the EC2 – blocked traffic won't reach the instance.
    
* **Best Practice:** Maintain a separate security group for SSH access.
    
* **Troubleshooting Tips:**
    
    * Timeout Issue: Likely a security group problem.
        
    * "Connection Refused" Error: Indicates an application error or non-launched state.
        
* **Defaults:**
    
    * All inbound traffic is blocked by default.
        
    * All outbound traffic is authorized by default.
        

## Referencing Other Security Groups: Strengthening Connections 🤝🔗

### Diagram: Creating Interlinked Security Groups

* **Components:**
    
    * EC2 Instances.
        
    * Multiple Security Groups.
        
    * Inbound Rules Authorizing Other Security Groups.
        

## Classic Ports to Master: Navigating the Digital Highway 🚢🔧

### Essential Ports:

* **22:** SSH (Secure Shell) – Linux instance login.
    
* **21:** FTP (File Transfer Protocol) – File upload into a file share.
    
* **22 (again):** SFTP (Secure File Transfer Protocol) – File upload using SSH.
    
* **80:** HTTP – Access unsecured websites.
    
* **443:** HTTPS – Access secured websites.
    
* **3389:** RDP (Remote Desktop Protocol) – Windows instance login.
    

## Conclusion: Empowering Your Network Security 🚀🔐

Understanding the role and functionality of security groups is pivotal for crafting a secure AWS environment. As the guardians of network security, security groups allow you to finely control traffic, regulate access, and fortify your EC2 instances against potential threats. Dive into the AWS console, configure your security groups, and navigate the digital realm with confidence! 🌐🛡️