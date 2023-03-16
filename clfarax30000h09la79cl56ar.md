---
title: "Understanding Version Control: Central vs Distributed Systems and Git vs GitHub"
datePublished: Thu Mar 16 2023 06:55:01 GMT+0000 (Coordinated Universal Time)
cuid: clfarax30000h09la79cl56ar
slug: understanding-version-control-central-vs-distributed-systems-and-git-vs-github
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1678950007832/b2afab68-0815-4380-842c-25a82b224e37.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1678957158623/a3a03e5b-5732-4423-93ee-3fba217d7d71.png
tags: github, python, developer, devops, beginners

---

# **📍 Introduction:**

Have you ever been in a situation where you lost an important piece of code or struggled to maintain different versions of your codebase? If yes, then version control might be the solution you're looking for. In this blog, we'll discuss what version control is, the differences between central and distributed version control systems, and the difference between Git and GitHub.

## **🔹**What's Version Control?

Version control is the process of managing and tracking changes made to a file or a set of files over time. It helps to achieve two main objectives: manageability and versioning of code. With version control, you can keep track of changes made to your codebase, collaborate with others, and maintain different versions of your code.

# **📍** Difference between Central and Distributed Version Control Systems:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678948065525/75110865-f22e-4b6a-8807-e04195022684.png align="center")

## **🔹 Central Version Control:**

Central version control systems help to maintain the central versioning of code within a central place inside an organization. However, it comes with a risk if the central server went down, then you won't be able to share the code with others. Examples of a central version control system are SVN.

## **🔹 Distributed Version Control:**

Distributed version control systems help to maintain the distributed versioning of code at different locations. So there is no risk of losing the source code, even if the central source code went down. In distributed version control systems, forking helps to maintain multiple copies of the main code at your level and work on it. At the end of the process, you can ask for a pull request (PR) to merge the changes back to the main central repository of the organization. Examples of distributed version control systems are Git & GitHub, Gitlab, and Bitbucket.

# **📍** Difference between Git and GitHub:

## **🔹 Git:**

Git is a local-level tool to manage our source code, and it's open source. Even we can build our own central version control system by launching an EC2 server and installing Git on it and managing the other system to sync our source code. Git has several crucial commands, including Git init, Git clone, Git status, Git add filename, Git commit -m "commit\_message", Git push, Git pull, Git diff, Git fetch, Git merge, and Git logs.

### **⚜ Git Commands:**

1. `git init`: Initializes a new Git repository in the current directory. Example: `git init`.
    
2. `git clone`: Copies an existing Git repository to your local machine. Example: `git clone` [`https://github.com/example/example.git`](https://github.com/example/example.git).
    
3. `git status`: Shows the current state of your Git repository, including any changes that have been made to your files. Example: `git status`.
    
4. `git add`: Adds changes made to specific files to the staging area, preparing them for commit. Example: `git add index.html`.
    
5. `git commit`: Saves changes made to the Git repository, along with a descriptive commit message. Example: `git commit -m "Added new feature"`.
    
6. `git push`: Uploads local changes to a remote Git repository. Example: `git push origin master`.
    
7. `git pull`: Downloads changes from a remote Git repository to your local machine. Example: `git pull origin master`.
    
8. `git diff`: Shows the differences between two versions of a file or between two branches. Example: `git diff HEAD~1 HEAD`.
    
9. `git fetch`: Downloads changes from a remote Git repository without merging them with your local repository. Example: `git fetch origin`.
    
10. `git merge`: Combines changes from one branch into another branch. Example: `git merge feature-branch`.
    
11. `git branch`: Shows a list of all branches in the Git repository. Example: `git branch`.
    
12. `git checkout`: Switches between different branches or commits in the Git repository. Example: `git checkout feature-branch`.
    
13. `git log`: Shows a history of all commits made to the Git repository. Example: `git log`.
    

## **🔹 GitHub:**

GitHub helps with usability, issue raising, commenting, reviewing, collaboration, project management, and CI/CD pipelines using GitHub Actions. With GitHub, you can easily collaborate with others, raise issues, communicate through commenting, review code changes, manage projects, and automate your CI/CD pipelines.

# **📍 Conclusion:**

In conclusion, version control is a crucial tool for managing and tracking changes made to a file or a set of files over time. It helps to maintain different versions of your codebase, collaborate with others, and keep track of changes made to your code. Central and distributed version control systems have their own advantages and disadvantages, and you can choose the one that fits your organization's requirements. Git and GitHub are popular tools for version control and collaboration, and they have unique features and functionalities.