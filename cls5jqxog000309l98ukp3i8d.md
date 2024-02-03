---
title: "Troubleshooting Linux Scenarios – Part 1"
datePublished: Sat Feb 03 2024 04:00:51 GMT+0000 (Coordinated Universal Time)
cuid: cls5jqxog000309l98ukp3i8d
slug: troubleshooting-linux-scenarios-part-1
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1706899814541/0e037486-7941-4dfe-8d84-0c96cca9393d.png
tags: linux, technology, python, web-development, kubernetes, developer, testing, devops, troubleshooting, linux-for-beginners, linux-basics, linux-commands, 90daysofdevops, trainwithshubham, 90daysofdevops-chanllenge

---

### Issue 1: Unable to Start a Service

🛠️ **Approach / Solution:**

```plaintext
├── Check if the service is installed
├── Verify the service configuration file
├── Check the service status using systemctl or other command
├── Inspect the service logs for any errors
├── Ensure there are no port conflicts
├── Review firewall rules and SELinux settings
├── Restart the service and check for error messages
├── Inspect system resource usage with tools like top or htop
└── ...
```

### Issue 2: High CPU Usage

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

### Issue 3: Network Connectivity Issues Between Servers

🛠️ **Approach / Solution:**

```plaintext
├── Check if other servers on the same network are accessible
├── Verify firewall rules on both source and destination servers
├── Inspect routing tables to ensure correct routes are set
├── Use tools like traceroute or mtr to trace the network path
├── Check for any network hardware failures or misconfigurations
├── Review system logs for network-related errors
├── Test connectivity using tools like telnet or nc
├── Investigate potential DNS or hostname resolution problems
├── Consider network segmentation or VLAN configurations
└── ...
```

### Issue 4: Unable to Mount a Filesystem

🛠️ **Approach / Solution:**

```plaintext
bash
```

```plaintext
├── Check if the filesystem is specified in /etc/fstab
├── Verify the device path and UUID in /etc/fstab
├── Ensure the filesystem type is correct
├── Check for errors in /var/log/messages or dmesg
├── Confirm that the device is accessible and not failing
├── Use the mount command manually to check for errors
├── Investigate if the filesystem needs repair (fsck)
├── Inspect disk space on the target mount point
├── Check for any SELinux or AppArmor restrictions
└── ...
```

### Issue 5: Filesystem corrupted

🛠️ **Approach / Solution:**

```plaintext
├── One of the error that causes the system unable to BOOT UP
├── Check /var/log/messages, dmesg, and other log files
├── If we have bad sector logs, we have to run fsck
│ ├── True:
│ │ ├── Reboot the system into rescue mode by booting it from CDROM by applying ISO
│ │ ├── Proceed with option 1, which mounts the original root filesystem under /mnt/sysimage
│ │ ├── Edit fstab entries or create a new file with the help of blkid and reboot
└── ...
```

### Issue 6: Can’t cd to the directory even if the user has sudo privileges

🛠️ **Approach / Solution:**

```plaintext
├── Reasons and Resolution
│ ├── Directory does not exist
│ ├── Pathname conflict: relative vs absolute path
│ ├── Parent directory permission/ownership
│ ├── Doesn't have executable permission on the target directory
│ ├── Hidden directory
└── ...
```

### Issue 7: Running Out of Memory

🛠️ **Approach / Solution:**

```plaintext
├── Types
│ ├── Cache (L1, L2, L3)
│ ├── RAM
│ │ ├── Usage
│ │ │ ├── #free -h
│ │ │ │ ├── Total (Total assigned memory)
│ │ │ │ ├── Used (Total actual used memory)
│ │ │ │ ├── Free (Actual free memory)
│ │ │ │ ├── Shared (Shared Memory)
│ │ │ │ ├── Buff/Cache (Pages cache memory)
│ │ │ │ ├── Available (Memory can be freed)
│ │ │ ├── /proc/meminfo
│ │ │ │ ├── file active
│ │ │ │ ├── file inactive
│ │ │ │ ├── anon active
│ │ │ │ ├── anon inactive
│ ├── Swap (Virtual Memory)
├── Resolution
│ ├── Identify the processes that are using high memory using top, htop, ps, etc.
│ ├── Check the OOM in logs and also check if there is a memory commitment in sysctl.conf
│ ├── Kill or restart the process/service
│ ├── Prioritize the process using nice
│ ├── Add/Extend the swap space
│ ├── Add more physical more RAM
└── ...
```

### Issue 8: Add/Extend the Swap Space

🛠️ **Approach / Solution:**

```plaintext
├── Due to running out of memory, we would need to add more swap space
│ ├── Create a file with #dd, as it will reserve the blocks of disk for the swap file
│ ├── Set permission 600 and give root ownership
│ ├── #mkswap
│ ├── Now Turned swap on #swapon
│ ├── fstab entry for persistence
└── ...
```

### Issue 9: Unable to Run Certain Commands

🛠️ **Approach / Solution:**

```plaintext
├── Troubleshooting and Resolution
│ ├── command
│ │ ├── Could be the system-related command which non-root user does not have the access
│ │ ├── Could be the user-defined script/command
│ ├── Troubleshooting
│ │ ├── permission/ownership of the command/script
│ │ ├── sudo permission
│ │ ├── absolute/relative path of command/script
│ │ ├── not defined in user $PATH variable
│ │ ├── command is not installed
│ │ ├── command library is missing or deleted
└── ...
```

### Issue 10: System Unexpectedly reboot and process restart?

🛠️ **Approach / Solution:**

```plaintext
├── Troubleshooting and Resolution
│ ├── System reboot/crash reasons
│ │ ├── CPU stress
│ │ ├── RAM stress
│ │ ├── Kernel fault
│ │ ├── Hardware fault
│ ├── Process restart
│ │ ├── System reboot
│ │ ├── Restart itself
│ │ ├── Watchdog application
│ │ │ ├── To prevent high stress on system resources
│ │ │ ├── If the application is causing stress, so it will restart or terminate
│ ├── Troubleshooting
│ │ ├── After logged in, check the status by using commands like uptime, top, dmesg, journalctl, iostat -xz 1
│ │ ├── syslog.log, boot.log, dmesg, messages.log, etc
│ │ ├── custom log path of application
│ │ ├── if not completely accessible, so take the virtual console like from ILO, IDRAC, etc
│ │ ├── open a case and reach out a vendor
└── ...
```