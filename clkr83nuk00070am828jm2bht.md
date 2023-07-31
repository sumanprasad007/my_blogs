---
title: "Day 1 of the Bash Scripting Challenge! 🚀 #TWSBashBlazeChallenge"
datePublished: Mon Jul 31 2023 18:48:07 GMT+0000 (Coordinated Universal Time)
cuid: clkr83nuk00070am828jm2bht
slug: day-1-of-the-bash-scripting-challenge-twsbashblazechallenge
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1690829057172/db25d781-823a-4ace-bd93-e1d078cb9277.png
tags: linux, developer, devops, shell, 90daysofdevops

---

## **📍 Introduction:**

Bash scripting is a powerful tool that allows DevOps engineers to automate tasks and perform various operations on their systems. Today, we will cover the basics of bash scripting to get you started on this exciting journey. By the end of this challenge, you will have created a single bash script that completes multiple tasks and demonstrates your understanding of the concepts covered. Let's dive in! 💻

## **Task 1: Comments ✍️**

In bash scripts, comments play a vital role in making the code more understandable and explaining its functionality. They begin with the `#` symbol. Let's create a bash script with comments explaining what the script does. 📝

```plaintext
#!/bin/bash

# DevOps Engineer: This is a bash script that demonstrates basic concepts of bash scripting.
# Task 1: Comments
# - In this task, we will use comments to explain the script.

# Output a welcome message to the user
echo "Welcome to Day 1 of the Bash Scripting Challenge!"
```

## **Task 2: Echo 🗣️**

The `echo` command is one of the simplest and most frequently used commands in bash scripting. It is used to display messages on the terminal. Let's create a bash script that uses `echo` to print a message of our choice. 📢

```plaintext
#!/bin/bash

# DevOps Engineer: Task 2: Echo
# - In this task, we will use the 'echo' command to print a message.

# Output a welcome message to the user
echo "Welcome to Day 1 of the Bash Scripting Challenge!"
```

## **Task 3: Variables 📦**

Variables in bash are used to store data and can be referenced by their name. In this task, we will create a bash script that declares variables and assigns values to them. 📝

```plaintext
#!/bin/bash

# DevOps Engineer: Task 3: Variables
# - In this task, we will declare and use variables.

# Declare variables and assign values
engineer_name="Prasad"
engineer_age=23
engineer_country="India"

# Output the values of variables
echo "Name: $engineer_name"
echo "Age: $engineer_age"
echo "Country: $engineer_country"
```

## **Task 4: Using Variables 🎛️**

Now that we have declared variables, let's use them to perform a simple task. In this task, we will create a bash script that takes two variables (numbers) as input and prints their sum using those variables. ➕

```plaintext
#!/bin/bash

# DevOps Engineer: Task 4: Using Variables
# - In this task, we will use variables to perform a calculation.

# Get user input for two numbers
read -p "Enter the first number: " num1
read -p "Enter the second number: " num2

# Calculate the sum of the two numbers
sum=$((num1 + num2))

# Output the result
echo "The sum of $num1 and $num2 is: $sum"
```

## **Task 5: Using Built-in Variables 🛠️**

Bash provides several built-in variables that hold useful information. In this task, we will create a bash script that utilizes at least three different built-in variables to display relevant information. 🧰

```plaintext
#!/bin/bash

# DevOps Engineer: Task 5: Using Built-in Variables
# - In this task, we will use built-in variables.

# Output the current user
echo "Current user: $USER"

# Output the hostname
echo "Hostname: $HOSTNAME"

# Output the current working directory
echo "Current directory: $PWD"
```

## **Task 6: Wildcards 🔍**

Wildcards are special characters used to perform pattern matching when working with files. In this task, we will create a bash script that utilizes wildcards to list all the files with a specific extension in a directory. 🌐

```plaintext
#!/bin/bash

# DevOps Engineer: Task 6: Wildcards
# - In this task, we will use wildcards to list files.

# Define the target directory
target_directory="/home/suman/devops_docs/"

# List all files with a specific extension in the target directory
echo "Files with the '.txt' extension:"
ls "$target_directory"/*.txt
```

### **🔍 Checkout GitHub Repository for projects:**

**🔗** [**github.com/sumanprasad007**](http://github.com/sumanprasad007)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690656559825/0474ff76-1d75-4ce0-93ea-1194d2444f74.png?auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

### **🔍 Check out my YouTube channel - Prasad Suman Mohan:**

%[https://youtu.be/3r3crvdr3GY]