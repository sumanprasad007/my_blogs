---
title: "User Account Management with Bash Scripting 🚀"
datePublished: Wed Aug 02 2023 17:23:59 GMT+0000 (Coordinated Universal Time)
cuid: clktzz60x000309jz7heufjde
slug: user-account-management-with-bash-scripting
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1690996774893/837a472b-8e03-430a-b8fe-4f9f77b71124.png
tags: linux, developer, devops, shell, 90daysofdevops

---

# **📍**Introduction:

Managing user accounts on a system is a critical administrative task. It involves creating, deleting, and resetting passwords for users. Performing these actions manually can be time-consuming and error-prone. In this blog, we'll explore how to automate these tasks using a Bash script, making user account management a breeze! 🎉

Real-life Example: Imagine you are a system administrator responsible for maintaining a multi-user environment, like a university computer lab or a small office network. Users frequently join or leave, and it's crucial to efficiently manage their accounts to ensure security and accessibility. By using our Bash script, you can easily create new accounts, delete old ones, and reset passwords with just a few simple commands. Let's dive into the details! 💻

### **🔍 Understanding each argument based functionality:**

### Step 1: Account Creation 👤

Our first task is to create a new user account. The Bash script will prompt you to enter the new username and password. But beware! If the username already exists, the script will gracefully notify you and exit without any harm.

💡 Example:

```plaintext
$ ./user_management.sh -c
Enter the new username: prasad
Enter the password for prasad:
User account 'prasad' created successfully. 🎉
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690995821927/4dde38a6-84ab-4b5e-b889-8b1749b686c9.png align="center")

### Step 2: Account Deletion ❌

Now, let's handle the account deletion process. You will be prompted to enter the username of the account to be deleted. If the provided username does not exist, the script will inform you and exit.

💡 Example:

```plaintext
$ ./user_management.sh -d
Enter the username to be deleted: prasad
User account 'prasad' deleted successfully. 👋
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690995847655/63a28483-334b-42da-94da-d4fb5516026a.png align="center")

### Step 3: Password Reset 🔑

Next, we'll implement the password reset feature. The script will ask for the username and the new password. If the username doesn't exist, the script will gracefully inform you and exit.

💡 Example:

```plaintext
$ ./user_management.sh -r
Enter the username for password reset: prasad
Enter the new password for prasad:
Password for user account 'prasad' reset successfully. 🔒
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690995877039/22730dfe-aba1-4ee2-a9af-6b1eca81b8dd.png align="center")

### Step 4: List User Accounts 📜

Now, let's create a way to list all user accounts on the system, along with their corresponding user IDs (UID).

💡 Example:

```plaintext
$ ./user_management.sh -l
Listing all user accounts:
Username: prasad       UID: 1001
Username: jane_smith     UID: 1002
Username: jdoe           UID: 1003
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690995902254/95a868c7-7c95-400d-87d1-d6515625aefc.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690995954807/0ab0ad47-a7dc-4c87-ab58-01970d11e1a6.png align="center")

### Step 5: Help and Usage Information ❓

Finally, we'll add a help option to display usage information and the available command-line options.

💡 Example:

```plaintext
$ ./user_management.sh -h
Usage: ./user_management.sh [OPTIONS]
Options:
  -c, --create  Create a new user account
  -d, --delete  Delete an existing user account
  -r, --reset   Reset the password of an existing user account
  -l, --list    List all user accounts on the system
  -h, --help    Display this help message
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690996091438/ce412c87-6636-4b27-a26e-b34e06ae49fa.png align="center")

Bonus Points! ✨ For those who wish to challenge themselves further, consider adding these bonus features to the script:

1. Displaying more detailed information about user accounts, such as the home directory, shell, etc.
    
2. Allowing the modification of user account properties, like username and user ID.
    

### **🔍** Fully functional shell script file:

```plaintext
#!/bin/bash

# Function to display usage information and available command-line options
function display_usage {
    echo "Usage: $0 [OPTIONS]"
    echo "Options:"
    echo "  -c, --create  Create a new user account"
    echo "  -d, --delete  Delete an existing user account"
    echo "  -r, --reset   Reset the password of an existing user account"
    echo "  -l, --list    List all user accounts on the system"
    echo "  -h, --help    Display this help message"
}

# Function to check if a user exists
function check_user_existence {
    local username=$1
    id "$username" &>/dev/null
    return $?
}

# Function to create a new user account
function create_user_account {
    read -p "Enter the new username: " new_username

    # Check if the username already exists
    if check_user_existence "$new_username"; then
        echo "Error: Username already exists. Please choose a different username."
        exit 1
    fi

    # Prompt for password and create the user
    read -s -p "Enter the password for $new_username: " new_password
    echo
    useradd "$new_username" --create-home --password "$new_password"

    echo "User account '$new_username' created successfully."
}

# Function to delete an existing user account
function delete_user_account {
    read -p "Enter the username to be deleted: " delete_username

    # Check if the username exists
    if ! check_user_existence "$delete_username"; then
        echo "Error: Username '$delete_username' does not exist."
        exit 1
    fi

    userdel -r "$delete_username"
    echo "User account '$delete_username' deleted successfully."
}

# Function to reset the password of an existing user account
function reset_user_password {
    read -p "Enter the username for password reset: " reset_username

    # Check if the username exists
    if ! check_user_existence "$reset_username"; then
        echo "Error: Username '$reset_username' does not exist."
        exit 1
    fi

    read -s -p "Enter the new password for $reset_username: " new_password
    echo
    echo "$reset_username:$new_password" | chpasswd

    echo "Password for user account '$reset_username' reset successfully."
}

# Function to list all user accounts on the system
function list_user_accounts {
    echo "Listing all user accounts:"
    awk -F: '{print "Username:",$1,"\tUID:",$3}' /etc/passwd
}

# Parse command-line options
while [[ "$1" != "" ]]; do
    case $1 in
        -c | --create)
            create_user_account
            ;;
        -d | --delete)
            delete_user_account
            ;;
        -r | --reset)
            reset_user_password
            ;;
        -l | --list)
            list_user_accounts
            ;;
        -h | --help)
            display_usage
            exit 0
            ;;
        *)
            echo "Error: Invalid option '$1'."
            display_usage
            exit 1
            ;;
    esac
    shift
done

# If no options provided, display usage information
if [[ "$#" -eq 0 ]]; then
    echo "Error: No options provided."
    display_usage
    exit 1
fi
```

Instructions for running the script:

1. Save the script in a file named `user_management.sh`.
    
2. Make the script executable: `chmod +x user_management.sh`.
    
3. Run the script with desired options. For example:
    
    * Create a new user: `./user_management.sh -c`
        
    * Delete an existing user: `./user_management.sh -d`
        
    * Reset user password: `./user_management.sh -r`
        
    * List all user accounts: `./user_management.sh -l`
        
    * Display help: `./user_management.sh -h`
        

### **🔍 Output Screens:**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690995785398/b24386f6-9e72-4291-98e8-2afb13e1a591.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690995772380/508cf98e-33ce-4a87-8193-b2c8c49e4d93.png align="center")

> Note: To execute some parts of the script (like adding or deleting users), you may need to run it with `sudo` or as a superuser, depending on your system's configuration and permissions.

# **📍** Conclusion:

By now, you have an efficient and powerful Bash script to manage user accounts on your system. Whether you're administering a small network or a large organization, this script will save you time and effort, ensuring smooth user account management. Happy scripting and managing user accounts! 🤗

### **🔍 Checkout GitHub Repository for projects:**

**🔗** [**github.com/sumanprasad007**](http://github.com/sumanprasad007)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690656559825/0474ff76-1d75-4ce0-93ea-1194d2444f74.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

### **🔍 Check out my YouTube channel - Prasad Suman Mohan:**

🔗 [**youtube.com/@sumanprasad007**](http://youtube.com/@sumanprasad007)

[![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690893614276/e567a0e4-c76d-4f49-b537-34ca8e727e5d.png?auto=compress,format&format=webp&auto=compress,format&format=webp align="left")](https://www.youtube.com/@sumanprasad007)