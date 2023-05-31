---
title: "CI/CD Pipeline for Node JS Application using GitHub Action"
datePublished: Wed May 31 2023 04:12:23 GMT+0000 (Coordinated Universal Time)
cuid: clib6yig600010alfbm11dd3e
slug: cicd-pipeline-for-node-js-application-using-github-action
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1685386740676/8626d685-5ef9-4fd4-a2bf-ff31b18f7f63.jpeg
tags: software-development, aws, web-development, developer, devops

---

# **📍** Introduction:

Continuous Integration and Continuous Deployment (CI/CD) are essential practices in modern software development. They help streamline the development process, reduce errors, and ensure that your application is always up-to-date. In this blog, we'll walk you through setting up a CI/CD pipeline for a Node.js application using GitHub Actions. We'll cover everything from creating a simple Node.js application to deploying it using GitHub Actions.

# 📝 Pre-requisites:

* A GitHub account
    
* Basic knowledge of Node.js and npm
    

### 🚀 Step 1: Create a Node.js application

First, let's create a simple Node.js application. Create a new directory for your project and navigate to it:

```plaintext
mkdir my-node-app
cd my-node-app
```

Initialize a new Node.js project with the following command:

```plaintext
bashCopynpm init -y
```

This command generates a **package.json** file with default values.

Create a new file called **index.js** and add the following content:

```plaintext
console.log('Hello, Node.js!');
```

### 🚀 Step 2: Initialize a Git repository

Initialize a Git repository in your project directory:

```plaintext
git init
```

Create a **.gitignore** file to exclude unnecessary files from the repository:

```plaintext
echo "node_modules/" > .gitignore
```

Commit the initial project files:

```plaintext
git add .
git commit -m "Initial commit"
```

### 🚀 Step 3: Create a GitHub repository

Create a new repository on GitHub and push your local repository to it:

```plaintext
git remote add origin https://github.com/your-username/my-node-app.git
git branch -M main
git push -u origin main
```

### 🚀 Step 4: Set up GitHub Actions

Create a new directory called **.github/workflows** in your project:

```plaintext
mkdir -p .github/workflows
```

Create a new file called **ci-cd.yml** inside the **.github/workflows** directory:

```plaintext
touch .github/workflows/ci-cd.yml
```

Open the **ci-cd.yml** file and add the following content:

```plaintext
name: Node.js CI/CD

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout repository
      uses: actions/checkout@v2

    - name: Set up Node.js
      uses: actions/setup-node@v2
      with:
        node-version: '14'

    - name: Cache npm dependencies
      uses: actions/cache@v2
      with:
        path: ~/.npm
        key: ${{ runner.os }}-node-${{ hashFiles('**/package-lock.json') }}
        restore-keys: ${{ runner.os }}-node

    - name: Install dependencies
      run: npm ci

    - name: Run tests
      run: npm test

    - name: Deploy
      if: github.ref == 'refs/heads/main'
      run: echo "Deploy your application here"
```

This GitHub Actions workflow does the following:

* Triggers on push and pull request events to the **main** branch
    
* Checks out the repository
    
* Sets up Node.js
    
* Caches npm dependencies for faster builds
    
* Installs dependencies using **npm ci**
    
* Runs tests (add your test script to **package.json**)
    
* Deploys the application (replace the **echo** command with your deployment script)
    

### 🚀 Step 5: Commit and push the GitHub Actions workflow

Add the new GitHub Actions workflow to your repository:

```plaintext
bashCopygit add .github/workflows/ci-cd.yml
git commit -m "Add GitHub Actions CI/CD workflow"
git push
```

Now, whenever you push changes to your **main** branch or create a pull request, the GitHub Actions workflow will automatically build, test, and deploy your Node.js application.

# 📍 Conclusion:

In this blog, we've demonstrated how to set up a CI/CD pipeline for a Node.js application using GitHub Actions. By following these steps, you can automate the build, test, and deployment processes for your Node.js projects, ensuring that your application is always up-to-date and error-free. Happy coding!

## **🔹 Checkout GitHub Repository for projects:**

**🔗** [**github.com/sumanprasad007**](http://github.com/sumanprasad007)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685387341757/a0c4ecb8-9b61-4008-94ab-d6418fda5fae.png align="center")