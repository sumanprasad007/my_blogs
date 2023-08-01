---
title: "Day 2: Exploring Files and Directories with Bash - #TWSBashBlazeChallenge🚀"
datePublished: Tue Aug 01 2023 13:00:40 GMT+0000 (Coordinated Universal Time)
cuid: clksb4pch000609mdaj75es1u
slug: day-2-exploring-files-and-directories-with-bash-twsbashblazechallenge
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1690894448572/4562b99d-4251-4c5a-b156-18b621fbc93d.png
tags: linux, azure, devops, shell, 90daysofdevops

---

# 📍 Introduction:

Welcome to Day 2 of the #TWSBashBlazeChallenge! Today's challenge focuses on building an interactive script that explores files and directories, while also performing character counting in Bash. We'll create a script called [`explorer.sh`](http://explorer.sh) that will provide you with a fun and interactive way to navigate through your files and directories, and even count characters in your input! Let's get started with some Bash magic! 🧙‍♂️

### **🔍** Part 1: File and Directory Exploration 👣

Upon running the [`explorer.sh`](http://explorer.sh) script without any command-line arguments, it will display a warm welcome message and list all the files and directories in the current path. 📂 For each file and directory, the script will print its name and size in human-readable format (e.g., KB, MB, GB). We'll accomplish this by using the `ls` command with appropriate options. Let's see how it's done! 🕵️‍♀️

### 📝 [explorer.sh](http://explorer.sh):

```plaintext
#!/bin/bash

# Part 1: File and Directory Exploration

# Welcome message
echo "Welcome to the Interactive File and Directory Explorer! 🌟"

# Infinite loop until the user decides to exit
while true; do
    # Display files and directories in the current path using ls command with human-readable sizes
    echo "Files and Directories in the Current Path:"
    ls -lh

    # Ask the user to enter a line of text
    echo -n "Enter a line of text (Press Enter without text to exit): "
    
    # Read user input into the variable 'input'
    read input

    # Check if the user entered an empty string (i.e., pressed Enter without any text)
    if [[ -z "$input" ]]; then
        echo "Exiting the Interactive Explorer. Goodbye! 👋"
        break   # Exit the loop if the user entered an empty string
    else
        # Count the number of characters in the input and display the count
        char_count=${#input}
        echo "Character Count: $char_count"
    fi
done

# End of script
```

### **🔍** Part 2: Character Counting 🧮

After displaying the file and directory list, the script will prompt you to enter a line of text. 📝 The script will keep reading your input until you provide an empty string (i.e., press Enter without any text). For each line of text entered, the script will count the number of characters and show you the character count. It's an excellent way to play with the script and see how many characters are in your input! 🎉

### **🔍** Usage:

1. Save the script in a file named [`explorer.sh`](http://explorer.sh).
    
2. Make the script executable using the command: `chmod +x` [`explorer.sh`](http://explorer.sh).
    
3. Execute the script using: `./`[`explorer.sh`](http://explorer.sh).
    

### **🔍** Output Screen:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690894276466/6b4d400a-10e3-4efd-b72f-449e00bb518c.png align="center")

# 📍 Conclusion:

Congratulations! You have successfully completed Day 2 of the #TWSBashBlazeChallenge. You now have a powerful and interactive script that allows you to explore files and directories in your current path, along with a handy character-counting feature. 🚀 I hope you had fun building this script and learning more about Bash scripting. Stay tuned for more exciting challenges in the upcoming days! Happy scripting and exploring! 🎈🌌

### **🔍 Checkout GitHub Repository for projects:**

**🔗** [**github.com/sumanprasad007**](http://github.com/sumanprasad007)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690656559825/0474ff76-1d75-4ce0-93ea-1194d2444f74.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

### **🔍 Check out my YouTube channel - Prasad Suman Mohan:**

🔗 [https://www.youtube.com/@sumanprasad007](https://www.youtube.com/@sumanprasad007)

[![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690893614276/e567a0e4-c76d-4f49-b537-34ca8e727e5d.png align="center")](https://www.youtube.com/@sumanprasad007)