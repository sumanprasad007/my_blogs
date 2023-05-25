---
title: "Understanding Terminologies associated with GitHub Action 📢"
datePublished: Thu May 25 2023 03:49:04 GMT+0000 (Coordinated Universal Time)
cuid: cli2lhet0000s09jt1uxp5qv2
slug: understanding-terminologies-associated-with-github-action
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1684900275374/0f829e9d-0796-4c68-8b02-a56ec63b3888.png
tags: aws, github, developer, devops, beginners

---

# **📍** Introduction:

GitHub Actions is a powerful automation tool that allows developers to automate tasks within their software development life cycle. It enables you to create custom workflows that can be triggered by various events, such as pushing code to a repository or creating a pull request. In this blog post, we will explore the key terminologies associated with GitHub Actions Workflow and provide examples to help even non-IT graduates understand the concepts.

## **🔹** Repository

A repository is a storage space where your project files, including code, documentation, and other assets, are stored. It is the central hub for your project, allowing you and your team to collaborate, track changes, and manage versions of your code.

Example: Imagine a repository as a digital folder containing all the files related to your project.

Syntax: A repository named "my-sample-project" contains the source code, documentation, and other files related to a web application.

## **🔹**Workflow

A workflow is a set of automated tasks or jobs that are executed based on specific triggers or events. In GitHub Actions, workflows are defined using YAML (Yet Another Markup Language) files, which are stored in the .github/workflows directory of your repository.

Example: Think of a workflow as a recipe that outlines the steps to be followed when a specific event occurs, such as baking a cake when it's someone's birthday.

Syntax: A workflow named "run-tests" is created to automatically run tests whenever new code is pushed to the "my-sample-project" repository. The workflow file, "run-tests.yml", is stored in the .github/workflows directory of the repository.

```plaintext
yamlCopyname: Run Tests

on: [push]

jobs:
  test:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout code
      uses: actions/checkout@v2

    - name: Set up Node.js
      uses: actions/setup-node@v2
      with:
        node-version: 14

    - name: Install dependencies
      run: npm ci

    - name: Run tests
      run: npm test
```

## **🔹** Actions

Actions are individual tasks that can be combined to create a workflow. They are reusable pieces of code that can be developed by you or shared by the community. Actions can be written in any programming language and can be used to perform various tasks, such as running tests, deploying code, or sending notifications.

Example: An action is like an ingredient in a recipe, each serving a specific purpose and contributing to the final result.

Syntax: In therun-tests" workflow, we use two pre-built actions: "actions/checkout@v2" to check out the repository's code and "actions/setup-node@v2" to set up the Node.js environment.

## **🔹** Events

Events are specific occurrences within a GitHub repository that can trigger a workflow. Examples of events include pushing code to a branch, creating a pull request, or opening an issue. You can configure your workflow to run on one or multiple events.

Example: An event is like a specific condition that, when met, initiates the execution of a workflow, such as starting a car when the key is turned.

Syntax: In the "run-tests" workflow, the event that triggers the workflow is "push", which means the workflow will run whenever new code is pushed to the repository.

```plaintext
yamlCopyon: [push]
```

## **🔹** Jobs

Jobs are a collection of steps that run sequentially within a workflow. Each job runs in a separate environment called a "runner," which can be a virtual machine or a container. Jobs can run in parallel or depend on the completion of other jobs.

Example: A job is like a stage in a multi-stage race, where each stage must be completed before moving on to the next.

Syntax: In the "run-tests" workflow, there is a single job named "test" that runs an Ubuntu environment and contains a series of steps to check out the code, set up Node.js, install dependencies, and run tests.

```plaintext
yamlCopyjobs:
  test:
    runs-on: ubuntu-latest

    steps:
    # Steps go here
```

## **🔹** Steps

Steps are individual tasks within a job. They can be either an action or a shell command. Steps are executed sequentially within a job, and each step can have its own set of inputs and outputs.

Example: A step is like a single instruction in a recipe, such as chopping vegetables or mixing ingredients.

Syntax: In the "test" job of the "run-tests" workflow, there are four steps:

* Checkout code
    
* Set up Node.js
    
* Install dependencies
    
* Run tests
    

Each step either uses an action or runs a shell command.

```plaintext
yamlCopysteps:
- name: Checkout code
  uses: actions/checkout@v2

- name: Set up Node.js
  uses: actions/setup-node@v2
  with:
    node-version: 14

- name: Install dependencies
  run: npm ci

- name: Run tests
  run: npm test
```

## **🔹 Runners**:

A runner is a server or virtual machine that executes the steps in a job. Runners can be hosted by GitHub or self-hosted on the user's own infrastructure. Runners can be used to run jobs in parallel, distribute workloads, and improve performance.

Example: A runner for a delivery company could be a truck or a bicycle. The runner could be used to deliver packages to multiple locations, optimize routes, and improve delivery times.

Syntax: In the "test" job of the "run-tests" workflow, the runner is specified as

ubuntu-latest", which means the job will run on the latest version of the Ubuntu operating system provided by GitHub-hosted runners.

```plaintext
yamlCopyruns-on: ubuntu-latest
```

## **🔹 Secrets**:

Secrets are encrypted variables that are used to store sensitive information, such as API keys or passwords. Secrets can be used in workflows to authenticate with external services or access protected resources. Secrets are stored securely and can be accessed only by authorized users.

Example: A secret for a bank could be a customer's account number or social security number. The secret could be used to authenticate with the bank's API and retrieve account information.

Syntax: In the "deploy-app" workflow, we use a secret named "HOSTING\_API\_KEY" to store the API key required for deploying the application to the hosting platform.

```plaintext
yamlCopy- name: Deploy to hosting platform
  run: deploy.sh
  env:
    API_KEY: ${{ secrets.HOSTING_API_KEY }}
```

To add a secret, go to your repository settings, click on "Secrets" in the left sidebar, and then click on "New repository secret" to create a new secret.

## **🔹 Environments**:

An environment is a named set of infrastructure resources, such as servers or databases, that are used for a specific purpose, such as testing or production. Environments can be used to manage infrastructure resources, deploy applications, and test code in a controlled environment.

Example: An environment for a movie theater could be the process of setting up the theater for a specific movie or event. The environment could include resources such as projectors, screens, and sound systems.

Syntax: In the "deploy-app" workflow, we set an environment variable named "APP\_ENV" at the job level, which is accessible in all steps of the job.

```plaintext
yamlCopyjobs:
  deploy:
    runs-on: ubuntu-latest
    environment:
      APP_ENV: production

    steps:
    # Steps go here
```

## **🔹 Artifacts**:

Artifacts are files that are produced by a job and can be used for further analysis or deployment. Artifacts can include build artifacts, test results, or deployment packages. Artifacts can be stored in GitHub or external storage systems.

Example: An artifact for a fashion company could be a design file or a product image. The artifact could be used to create a prototype, test the design, or showcase the product to customers.

Syntax: In the "build-and-deploy" workflow, we create an artifact named "build-output" that contains the compiled application files. This artifact can be used in a subsequent job or downloaded for further analysis.

```plaintext
yamlCopyjobs:
  build:
    runs-on: ubuntu-latest

    steps:
    # Steps to build the application go here

    - name: Upload build output as artifact
      uses: actions/upload-artifact@v2
      with:
        name: build-output
        path: dist/

  deploy:
    needs: build
    runs-on: ubuntu-latest

    steps:
    - name: Download build output artifact
      uses: actions/download-artifact@v2
      with:
        name: build-output

    # Steps to deploy the application go here
```

In this example, the "build" job compiles the application and uploads the output as an artifact. The "deploy" job then downloads the artifact and proceeds with the deployment process. By understanding and utilizing secrets, environment variables, and artifacts, you can create more efficient and secure workflows in your software development process.

## **📍** Conclusion:

Understanding the terminologies associated with GitHub Actions Workflow is crucial for effectively utilizing this powerful automation tool. By grasping the concepts of repositories, workflows, actions, events, jobs, steps, and runners, even non-IT graduates can harness the power of GitHub Actions to automate tasks and streamline their projects. By understanding these key topics, users can effectively use GitHub Actions to automate their software development workflows and improve their development process.

## **🔹 Image Credit:** [Digging into GitHub Actions](https://www.google.com/url?sa=i&url=https%3A%2F%2Fwww.liatrio.com%2Fblog%2Fgithub-actions&psig=AOvVaw27vIDri57mSBm9wzMYwFkx&ust=1684986578260000&source=images&cd=vfe&ved=0CBMQjhxqFwoTCJDMraWGjf8CFQAAAAAdAAAAABAg)

## **🔹 Checkout GitHub Repository for projects:**

**🔗** [**github.com/sumanprasad007**](http://github.com/sumanprasad007)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684899141513/510cba9d-0510-463d-9d00-4f0bfe130ed6.png?auto=compress,format&format=webp align="left")