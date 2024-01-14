---
title: "Day 22: Amazon RDS 🌊🔍"
datePublished: Sun Jan 14 2024 04:00:14 GMT+0000 (Coordinated Universal Time)
cuid: clrcyx3ys000109l97hsehjb6
slug: day-22-amazon-rds
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1705167433658/85815121-7df4-4e14-8f0b-40da38d7c28f.gif
tags: linux, docker, aws, python, development, web-development, kubernetes, developer, python3, devops, aws-lambda, aws-certified-solutions-architect-associate, 90daysofdevops, trainwithshubham

---

## Introduction 🗺️🚢

Dive into the seas of Amazon RDS (Relational Database Service), where managed databases take the helm, steering through the SQL realm. Explore the advantages, scaling capabilities, and disaster recovery features that make RDS a sailor's delight.

## Amazon RDS Overview 🚀💽

### Relational Database Symphony

RDS, or Relational Database Service, orchestrates databases in the cloud with seamless management for SQL-based databases:

* Postgres
    
* MySQL
    
* MariaDB
    
* Oracle
    
* Microsoft SQL Server
    
* Aurora (AWS Proprietary database)
    

## Advantage over using RDS versus deploying DB on EC2 🛡️🔧

### The Managed Advantage

Choosing RDS over manual deployment on EC2 comes with perks:

* Automated provisioning and OS patching
    
* Continuous backups with point-in-time restore
    
* Monitoring dashboards for insight
    
* Read replicas for enhanced read performance
    
* Multi-AZ setup for Disaster Recovery (DR)
    
* Hassle-free scaling (vertical and horizontal)
    

## RDS – Storage Auto Scaling 🔄📈

### Dynamic Storage Solutions

RDS Storage Auto Scaling ensures your database storage scales dynamically, preventing manual interventions. By setting maximum storage thresholds, RDS automatically adjusts storage when free storage is low, enhancing adaptability to unpredictable workloads.

## RDS Read Replicas for Read Scalability 📚🔄

### Replica Symphony

RDS Read Replicas bring harmony to read scalability:

* Up to 15 Read Replicas within AZ, Cross AZ, or Cross Region
    
* ASYNC replication ensures eventual consistency
    
* Replicas can be promoted to standalone DBs
    
* Ideal for read-heavy workloads, keeping the production DB unaffected
    

## RDS Multi AZ (Disaster Recovery) ☂️🔄

### Disaster-Proofing

RDS Multi AZ ensures disaster recovery with synchronous replication:

* SYNC replication for automatic failover
    
* Enhances availability, guarding against AZ, network, or instance failures
    
* Read Replicas can be part of Multi AZ setup for DR
    

## RDS Custom 🧰🛠️

### Tailored Database Experience

For the ultimate customization, RDS Custom offers access to OS and database settings:

* Managed Oracle and Microsoft SQL Server with customization
    
* Full admin access to the underlying OS and database
    
* Configure settings, install patches, enable native features
    
* Access the underlying EC2 Instance using SSH or SSM Session Manager
    

## Conclusion 🌊⚓

In the vast ocean of AWS, Amazon RDS emerges as a captain, steering your databases with finesse. With advantages, scalability, and disaster recovery features, RDS sets sail to make your database management voyage a breeze. ⛵🌐