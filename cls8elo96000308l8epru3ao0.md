---
title: "Part 2 - Troubleshooting Linux Scenarios 🧑‍💻"
datePublished: Mon Feb 05 2024 04:00:06 GMT+0000 (Coordinated Universal Time)
cuid: cls8elo96000308l8epru3ao0
slug: part-2-troubleshooting-linux-scenarios
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1707041406297/a1dd87fa-2024-4432-b311-e64b520ec344.png
tags: programming-blogs, linux, technology, python, web-development, security, kubernetes, developer, testing, devops, technical-writing-1, linux-for-beginners, 90daysofdevops, trainwithshubham

---

### **Issue 1: Unable to connect to a website or an application**

🛠️ **Approach / Solution:**

```plaintext
├── Ping the server by Hostname and IP Address
│ ├── False: Above Troubleshooting Diagram "Server is not reachable or cannot connect"
│ ├── True: Check the service availability by using telnet command with port
│ │ ├── True: Service is running
│ │ ├── False: Service is not reachable or running
│ │ │ ├── 📝 Check the service status using systemctl or other command
│ │ │ ├── 📝 Check the firewall/selinux
│ │ │ ├── 📝 Check the service logs
│ │ │ ├── 📝 Check the service configuration
└── ...
```

### Issue 2: Unable to get IP Address

```plaintext
🛠️ Approach / Solution:
├── IP Assignment Methods
│ ├── DHCP
│ │ ├── Fixed Allocation
│ │ ├── Dynamic Allocation
│ ├── Static
├── Troubleshooting
│ ├── check network setting from virtualization environment like VMware, VirtualBox, or etc
│ ├── check the IP address is assigned or not
│ ├── check the NIC status from the host side using #lspci, #nmcli, etc
│ ├── restart network service
└── ...
```

### Issue 3: Server is not reachable or unable to connect

🛠️ **Approach / Solution:**

```plaintext
├── Ping the server by Hostname and IP Address
│ ├── Hostname/IP Address is pingable
│ │ ├── Issue might be on the client side as server is reachable
│ ├── Hostname is not pingable but IP Address is pingable
│ │ ├── Could be the DNS issue
│ │ │ ├── 📝 check /etc/hosts
│ │ │ ├── 📝 check /etc/resolv.conf
│ │ │ ├── 📝 check /etc/nsswitch.conf
│ │ │ ├── (Optional) DNS can also be defined in the /etc/sysconfig/network-scripts/ifcfg-<interface>
│ ├── Hostname/IP Address both are not pingable
│ │ ├── Check the other server on its same network to see if there is a Network side access issue or overall something bad
│ │ │ ├── False: Issue is not overall network side but it's with that host/server
│ │ │ ├── True: Might be an overall network side issue
│ │ ├── Logged into the server by Virtual Console, if the server is Powered ON. Check the uptime
│ │ ├── Check if the server has the IP and has UP status of Network interface
│ │ │ ├── (Optional) Also check IP-related information from /etc/sysconfig/network-scripts/ifcfg-<interface>
│ │ ├── Ping the gateway, also check routes
│ │ ├── Check Selinux, Firewall rules
│ │ ├── Check physical cable connection
```

### **Issue 4: Unable to ssh as root or any other user**

```plaintext
🛠️ Approach / Solution:
├── Ping the server by Hostname and IP Address
│ ├── False: Above Troubleshooting Diagram "Server is not reachable or cannot connect"
│ ├── True: Check the service availability by using telnet command with port
│ │ ├── True: Service is running
│ │ │ ├── Issue might be on the client side
│ │ │ ├── User might be disabled, nologin shell, disabled root login, and other configurations
│ │ ├── False: Service is not reachable or running
│ │ │ ├── 📝 Check the service status using systemctl or other command
│ │ │ ├── 📝 Check the firewall/selinux
│ │ │ ├── 📝 Check the service logs
│ │ │ ├── 📝 Check the service configuration
└── ...
```

### Issue 5: Disk Space is full issue or add/extend disk space

🛠️ **Approach / Solution:**

```sql
├── System Performance degradation detection
│ ├── Application getting slow/unresponsive
│ ├── Commands are not running (For Example: / disk space is full)
│ ├── Cannot do logging and other etc
├── Analyse the issue
│ ├── df command to find the problematic filesystem space issue
├── Action
│ ├── After finding the specific filesystem, use du command in that filesystem to get which files/directories are large
│ ├── Compress/remove big files
│ ├── Move the items to another partition/server
│ ├── Check the health status of the disks using badblocks command (For Example: #badblocks -v /dev/sda)
│ ├── Check which process is IO Bound (using iostat)
│ ├── Create a link to file/dir
├── New disk addition
│ ├── Simple partition
│ │ ├── Add disk to VM
│ │ ├── Check the new disk with df/lsblk command
│ │ ├── fdisk to create partition. Better to have LVM partition
│ │ ├── Create filesystem and mount it
│ │ ├── fstab entry for persistence
│ ├── LVM Partition
│ │ ├── Add disk to VM
│ │ ├── Check the new disk with df/lsblk command
│ │ ├── fdisk to create LVM partition
│ │ ├── PV, VG, LV
│ │ ├── Create filesystem and mount it
│ │ ├── fstab entry for persistence
│ ├── Extend LVM partition
│ │ ├── Add disk, and create LVM partition
│ │ ├── Add LVM partition (PV) in the existing VG
│ │ ├── Extend LV and resize filesystem
└── ...
```

### Issue 6: SSL/TLS Certificate Expiry

🛠️ **Approach / Solution:**

```plaintext
├── Check SSL/TLS certificate expiration date
├── Confirm the correct certificate is being used
├── Renew the SSL/TLS certificate before expiry
├── Verify that the server's system time is accurate
├── Restart the web server after certificate renewal
├── Ensure the renewed certificate is properly configured
├── Check for any errors in the web server logs
├── Consider automating certificate renewal tasks
├── Monitor SSL/TLS certificate expiry using alerts
└── ...
```

### Issue 7: Database Connection Issue

🛠️ **Approach / Solution:**

```plaintext
├── Check if the database service is running
├── Verify database connection parameters (username, password)
├── Test database connectivity using command-line tools
├── Inspect database logs for connection errors
├── Review firewall rules for database port access
├── Confirm network accessibility between application and database servers
├── Check for any recent changes in the database configuration
├── Monitor database resource usage and performance
├── Investigate potential database server load issues
└── ...
```

### Issue 8: Web Application 404 Error

🛠️ **Approach / Solution:**

```plaintext
├── Verify that the requested URL is correct
├── Check web server logs for 404 error details
├── Confirm that the file or resource exists on the server
├── Review web server configuration for correct document root
├── Inspect file and directory permissions
├── Clear web browser cache and retry
├── Consider URL rewriting rules if applicable
├── Test with different browsers or devices
├── Investigate if there are any recent website changes
└── ...
```

### **Issue 9: Slow Application Response Time**

```plaintext
🛠️ Approach / Solution:
├── Identify bottlenecks using 'top' or 'htop'
├── Monitor application-specific logs for errors or warnings
├── Check for database connection and query performance
├── Review application code for inefficient algorithms
├── Optimize database queries and indexing
├── Investigate potential issues with external API calls
├── Monitor network latency between application components
├── Consider implementing caching mechanisms
├── Optimize server and network configurations
└── ...
```

### Issue 10: High CPU Usage

🛠️ **Approach / Solution:**

```plaintext
├── Identify the process causing high CPU usage using top or htop
├── Check if the issue is intermittent or continuous
├── Review logs for any error messages or known issues
├── Inspect running processes and their resource consumption
├── Investigate potential malware or unauthorized processes
├── Consider optimizing or scaling the application
├── Monitor system metrics over time to identify patterns
├── Apply performance tuning based on the specific application
└── ...
```