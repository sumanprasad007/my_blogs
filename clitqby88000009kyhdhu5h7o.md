---
title: "GitHub Action CI/CD Pipeline for Go Application"
datePublished: Tue Jun 13 2023 03:34:34 GMT+0000 (Coordinated Universal Time)
cuid: clitqby88000009kyhdhu5h7o
slug: github-action-cicd-pipeline-for-go-application
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1686627016459/0d178b3f-c265-4b1b-a3e5-acd465dddc16.jpeg
tags: aws, go, developer, devops, beginners

---

# 🚀 Introduction

It is a software practice that involves automating the building, testing, and deployment of code changes. By implementing a CI/CD pipeline, developers can ensure that their code is always in a releasable state and can be deployed to production quickly and reliably.

In this tutorial, we will walk through the steps to set up a CI/CD pipeline for a Go application using GitHub Actions. We will cover the following topics:

* Setting up a Go application
    
* Creating a GitHub repository
    
* Setting up a GitHub Actions workflow to build and test the application
    
* Setting up a GitHub Actions workflow to deploy the application to a server
    

### 👨‍💻 Prerequisites Before we get started, make sure you have the following:

* A GitHub account
    
* A server to deploy the application to (we will be using an Ubuntu 20.04 server for this tutorial)
    
* Git installed on your local machine and server
    

### 🏗️ Setting up a Go application

First, let's create a simple Go application that we can use for this tutorial. Create a new directory for the application and create a file called **main.go** with the following contents:

```plaintext
package main

import "fmt"

func main() {
    fmt.Println("Hello, world!")
}
```

This is a simple "Hello, world!" application that we will use to demonstrate the CI/CD pipeline.

Next, let's create a **go.mod** file to manage the application's dependencies. Run the following command in the application directory:

```plaintext
go mod init example.com/myapp
```

This will create a new **go.mod** file with the module name [**example.com/myapp**](http://example.com/myapp).

### 📦 Creating a GitHub repository

Next, let's create a new GitHub repository for the application. Log in to your GitHub account and click the "New" button to create a new repository. Give the repository a name and click "Create repository".

Once the repository is created, clone it to your local machine using the following command:

```plaintext
git clone https://github.com/<username>/<repository>.git
```

Replace **&lt;username&gt;** and **&lt;repository&gt;** with your GitHub username and the name of the repository you just created.

### 🔨 Setting up a GitHub Actions - Build & Test

workflow to build and test the application Now that we have a Go application and a GitHub repository, let's set up a GitHub Actions workflow to build and test the application.

Create a new directory called **.github/workflows** in the root of the repository, and create a file called **build-test.yml** with the following contents:

```plaintext
name: Build and Test

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v2

    - name: Set up Go
      uses: actions/setup-go@v2
      with:
        go-version: 1.16

    - name: Install dependencies
      run: go mod download

    - name: Build
      run: go build -v ./...

    - name: Test
      run: go test -v ./...
```

This workflow file specifies that the workflow should run when changes are pushed to the main branch of the repository. It defines a single job called "build" that runs on an Ubuntu virtual machine. The job consists of five steps:

* Checkout the repository code using the **actions/checkout** action.
    
* Set up Go on the virtual machine using the **actions/setup-go** action.
    
* Install dependencies using the **go mod download** command.
    
* Build the application using the **go build** command.
    
* Test the application using the **go test** command.
    

Commit the changes to the repository and push them to GitHub:

```plaintext
git add .
git commit -m "Add GitHub Actions workflow"
git push origin main
```

This will trigger the GitHub Actions workflow to build and test the application.

### 🚀 Setting up a GitHub Actions workflow to deploy

It helps to deploy the application to a server Now that we have a GitHub Actions workflow to build and test the application, let's set up a workflow to deploy the application to a server.

First, let's create a new directory called **deploy** in the root of the repository. In this directory, create a file called [**deploy.sh**](http://deploy.sh) with the following contents:

```plaintext
#!/bin/bash

set -e

ssh -i /path/to/private/key user@server "sudo systemctl stop myapp.service"

scp -i /path/to/private/key ./myapp user@server:/tmp/myapp

ssh -i /path/to/private/key user@server "sudo mv /tmp/myapp /usr/local/bin/myapp"
ssh -i /path/to/private/key user@server "sudo chmod +x /usr/local/bin/myapp"

ssh -i /path/to/private/key user@server "sudo systemctl start myapp.service"
```

This script will deploy the **myapp** binary to the server and restart the **myapp.service** systemd unit.

Next, let's create a new GitHub Actions workflow to deploy the application. Create a file called **deploy.yml** in the **.github/workflows** directory with the following contents:

```plaintext
name: Deploy

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v2

    - name: Set up
      uses: webfactory/ssh-agent@v0.5.0
      with:
        ssh-private-key: ${{ secrets.SSH_PRIVATE_KEY }}

    - name: Deploy
      run: |
        cd deploy
        ./deploy.sh
```

This workflow file specifies that the workflow should run when changes are pushed to the main branch of the repository. It defines a single job called "deploy" that runs on an Ubuntu virtual machine. The job consists of three steps:

* Checkout the repository code using the **actions/checkout** action.
    
* Set up SSH on the virtual machine using the **webfactory/ssh-agent** action and the **SSH\_PRIVATE\_KEY** secret.
    
* Deploy the application using the [**deploy.sh**](http://deploy.sh) script.
    

Commit the changes to the repository and push them to GitHub:

```plaintext
git add .
git commit -m "Add deploy script and workflow"
git push origin main
```

This will trigger the GitHub Actions workflow to deploy the application to the server.

# 🎉 Conclusion

Congratulations! You have successfully set up a CI/CD pipeline for a Go application using GitHub Actions. With this pipeline in place, you can easily build, test, and deploy your application with confidence.

### **🔹 Checkout GitHub Repository for projects:**

**🔗** [**github.com/sumanprasad007**](http://github.com/sumanprasad007)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686457356803/ab3e6329-34da-44a7-a1e8-8cbb426200b8.png?auto=compress,format&format=webp&auto=compress,format&format=webp align="left")