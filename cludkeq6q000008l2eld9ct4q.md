---
title: "Step by Step guide for Cron Jobs"
datePublished: Sat Mar 30 2024 04:00:55 GMT+0000 (Coordinated Universal Time)
cuid: cludkeq6q000008l2eld9ct4q
slug: step-by-step-guide-for-cron-jobs
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1711734948161/323a36d0-e42a-4eff-9122-968bdf83ab8e.jpeg
tags: linux, docker, python, web-development, kubernetes, webdev, developer, devops, frontend-development, linux-for-beginners, shell-script, devops-articles, 90daysofdevops, trainwithshubham

---

### What is a Cron Job?

Cron is a time-based job scheduler in Unix-like operating systems. It allows users to schedule jobs (commands or shell scripts) to run periodically at fixed times, dates, or intervals.

### Components of a Cron Job:

A cron job consists of:

1. **Schedule Expression:** Defines when the job should run. It includes minute, hour, day of the month, month, and day of the week fields.
    
2. **Command or Script:** The actual task or command that should be executed.
    

### Basic Syntax of a Cron Job:

```plaintext
* * * * * command_to_be_executed
| | | | |
| | | | +----- Day of the Week (0 - 6) (Sunday to Saturday)
| | | +------- Month (1 - 12)
| | +--------- Day of the Month (1 - 31)
| +----------- Hour (0 - 23)
+------------- Minute (0 - 59)
```

### Example: Scheduling a Cron Job

Let's schedule a simple cron job that echoes a message to a file every day at 2:30 PM.

Open your crontab file for editing:

* ```plaintext
      crontab -e
    ```
    
    `Choose the nano editor & paste the below job`
    
* Add the following line to schedule the job:
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1711734095228/e41ebf6f-159d-4b99-910d-ebda785490fe.png align="center")
    

1. ```plaintext
     30 14 * * * echo "Hello, this is a cron job!" >> /tmp/logfile.txt
    ```
    
    This expression means the job will run at 2:30 PM every day.
    
2. Save and exit the editor. (for nano `ctrl+x` & press `y)`
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1711734154850/42de6c88-6c27-4fad-a7d2-89ff66d9b1e9.png align="center")
    

### Real-Time Example:

Let's consider a real-time example. Suppose you have a backup script that you want to run every day at midnight.

1. Create a backup script, for example, [`backup.sh`](http://backup.sh):
    

* ```plaintext
      #!/bin/bash
      tar -czvf /Users/prasad/Documents/backup_$(date +\%Y\%m\%d_\%H\%M\%S).tar.gz /tmp/backup_directory
    ```
    
    This script creates a compressed backup file with a timestamp.
    
* Make the script executable:
    
* ```plaintext
      chmod +x backup.sh
    ```
    
* Open your crontab file:
    
* ```plaintext
      vi crontab -e
    ```
    
* Add the following line to schedule the backup script every day at midnight:
    
* ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1711734371092/a67652ea-bde1-4212-b724-a479e1098626.png align="center")
    

1. ```plaintext
     0 0 * * * /tmp/backup.sh
    ```
    
    This expression means the job will run at midnight (00:00) every day.
    
2. Save and exit the editor.
    

Now, your backup script will automatically run every day at midnight.

### Viewing Existing Cron Jobs:

To view your existing cron jobs, use the following command:

```plaintext
crontab -l
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1711734621749/e54b54fc-6377-48b8-bae6-8c8c2034d04d.png align="center")

### Important Tips:

* Each user has their own crontab, so cron jobs are specific to individual users.
    
* Be cautious while editing the crontab file, as an incorrect syntax can lead to issues.
    
* Use absolute paths in your cron jobs to avoid any issues related to the working directory.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1711734486712/699bf563-89dd-40ca-a244-465bcc23b35b.png align="center")

### Image Credit:

👨🏻‍💻 [https://nil.pro.np/set-up-cron-job-linux/](https://nil.pro.np/set-up-cron-job-linux/)