---
title: "Day 23: RDS Backups and Restoration 🔄🚀"
datePublished: Tue Jan 16 2024 04:00:51 GMT+0000 (Coordinated Universal Time)
cuid: clrfttl8x000809jm9ch9b7if
slug: day-23-rds-backups-and-restoration
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1705329831941/efc88304-4cf2-4306-9f0a-9d09b9d3c978.gif
tags: tutorial, linux, aws, technology, python, web-development, webdev, developer, devops, rdbms, aws-lambda, technical-writing-1, aws-certified-solutions-architect-associate, 90daysofdevops, trainwithshubham

---

## Introduction 🌟🚧

Embark on a voyage through the cosmos of RDS (Relational Database Service) backups and restoration, unraveling the intricacies of automated backups, manual snapshots, and the celestial Aurora database. As we navigate this journey, discover the art of data preservation and the various options for restoring databases.

![Managed disaster recovery with Amazon RDS for SQL Server using cross-Region  automated backups | AWS Database Blog](https://d2908q01vomqb2.cloudfront.net/887309d048beef83ad3eabf2a79a64a389ab1c9f/2021/07/07/DBB-1691-diag.png align="left")

## RDS Backups 📅💾

### Automated Backups

* Daily full backup during the backup window
    
* Transaction logs backed up every 5 minutes
    
* Point-in-time recovery from the oldest backup to 5 minutes ago
    
* Retention of 1 to 35 days (set 0 to disable automated backups)
    

![Automate the RDS backup function using Lambda | by Kubernetes Advocate |  AVM Consulting Blog | Medium](https://miro.medium.com/v2/resize:fit:1400/1*pD4y5ujVfoAArLsQi5dgAg.jpeg align="left")

### Manual DB Snapshots

* User-triggered snapshots
    
* Retention for as long as desired
    
* Tip: In a stopped RDS database, consider snapshotting & restoring to save on storage costs.
    

## Aurora Backups 📈💠

### Automated Backups

* Retention for 1 to 35 days (cannot be disabled)
    
* Point-in-time recovery within the retention timeframe
    

### Manual DB Snapshots

* User-triggered with retention flexibility
    

## Restore Options 🔄🔍

![Amazon RDS for SQL Server - Encrypted Backup/Restore - ⋮IWConnect](https://iwconnect.com/wp-content/uploads/1.jpg align="left")

### RDS & Aurora Restore Options

* Restoration creates a new database
    
* MySQL RDS Database Restore from S3
    
    * Backup on-premises database
        
    * Store on Amazon S3
        
    * Restore onto a new RDS instance running MySQL
        
* MySQL Aurora Cluster Restore from S3
    
    * Backup on-premises database using Percona XtraBackup
        
    * Store on Amazon S3
        
    * Restore onto a new Aurora cluster running MySQL
        

## Aurora Database Cloning 🌐🔧

### Swift Replication

* Create a new Aurora DB Cluster from an existing one
    
* Faster than snapshot & restore
    
* Utilizes the copy-on-write protocol
    
* Initially shares the same data volume as the original cluster
    
* Allocates additional storage and separates data when updates occur
    
* Swift, cost-effective, and ideal for staging databases without impacting production
    

## Conclusion 🌌⚖️

As we conclude this cosmic exploration, RDS and Aurora unveil their sophisticated backup and restoration mechanisms. From automated backups painting a daily canvas of data resilience to Aurora's swift cloning for staging, the celestial databases offer a symphony of options. May your data be secure, restorable, and ready for the next cosmic adventure! 🚀🛰️

### Image Credits:

* [https://www.google.com/url?sa=i&url=https%3A%2F%2Faws.amazon.com%2Fblogs%2Fdatabase%2Fmanaged-disaster-recovery-with-amazon-rds-for-sql-server-using-cross-region-automated-backups%2F&psig=AOvVaw3Vk0JYjuzEkJFk8wSOmbs0&ust=1705416089355000&source=images&cd=vfe&opi=89978449&ved=0CBMQjRxqFwoTCLCpoZbQ34MDFQAAAAAdAAAAABAg](https://www.google.com/url?sa=i&url=https%3A%2F%2Faws.amazon.com%2Fblogs%2Fdatabase%2Fmanaged-disaster-recovery-with-amazon-rds-for-sql-server-using-cross-region-automated-backups%2F&psig=AOvVaw3Vk0JYjuzEkJFk8wSOmbs0&ust=1705416089355000&source=images&cd=vfe&opi=89978449&ved=0CBMQjRxqFwoTCLCpoZbQ34MDFQAAAAAdAAAAABAg)
    
* [https://www.google.com/url?sa=i&url=https%3A%2F%2Fiwconnect.com%2Famazon-rds-for-sql-server-encrypted-backuprestore%2F&psig=AOvVaw3Vk0JYjuzEkJFk8wSOmbs0&ust=1705416089355000&source=images&cd=vfe&opi=89978449&ved=0CBMQjRxqFwoTCLCpoZbQ34MDFQAAAAAdAAAAABAY](https://www.google.com/url?sa=i&url=https%3A%2F%2Fiwconnect.com%2Famazon-rds-for-sql-server-encrypted-backuprestore%2F&psig=AOvVaw3Vk0JYjuzEkJFk8wSOmbs0&ust=1705416089355000&source=images&cd=vfe&opi=89978449&ved=0CBMQjRxqFwoTCLCpoZbQ34MDFQAAAAAdAAAAABAY)
    
* [https://www.google.com/url?sa=i&url=https%3A%2F%2Fmedium.com%2Favmconsulting-blog%2Fautomate-the-rds-backup-function-using-lambda-55c6e6857745&psig=AOvVaw3Vk0JYjuzEkJFk8wSOmbs0&ust=1705416089355000&source=images&cd=vfe&opi=89978449&ved=0CBMQjRxqFwoTCLCpoZbQ34MDFQAAAAAdAAAAABAn](https://www.google.com/url?sa=i&url=https%3A%2F%2Fmedium.com%2Favmconsulting-blog%2Fautomate-the-rds-backup-function-using-lambda-55c6e6857745&psig=AOvVaw3Vk0JYjuzEkJFk8wSOmbs0&ust=1705416089355000&source=images&cd=vfe&opi=89978449&ved=0CBMQjRxqFwoTCLCpoZbQ34MDFQAAAAAdAAAAABAn)