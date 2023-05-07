---
title: "Setting up a Self-Hosted GitHub Action Runner for Python Applications on EC2 Instance"
datePublished: Sun May 07 2023 03:00:39 GMT+0000 (Coordinated Universal Time)
cuid: clhcttt2y04r8m0nv4a3211mc
slug: setting-up-a-self-hosted-github-action-runner-for-python-applications-on-ec2-instance
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1683397200433/5af92140-7b5c-4205-b114-edd4811b643a.png
tags: software-development, aws, devops, beginners, patrimonio-de-venezuela

---

# **📍 Introduction:**

GitHub Actions is a powerful and flexible platform for automating software development workflows. With GitHub Actions, developers can easily build, test, and deploy their code directly from their GitHub repositories. GitHub provides two types of runners: GitHub-hosted runners and self-hosted runners. In this blog post, we will focus on the benefits of using self-hosted runners for Python applications and how to set them up using an EC2 instance.

# **📍** GitHub Hosted Runner vs Self-Hosted Runner

GitHub-hosted runners are provided by GitHub and run in a virtual machine hosted on GitHub infrastructure. They are free to use and support various operating systems, including Linux, Windows, and macOS. However, they have certain limitations, such as not allowing custom software installations, not having access to on-premises resources, and being subject to timeouts and usage limits.

On the other hand, self-hosted runners are runners that you set up and manage in your own infrastructure. With self-hosted runners, you have full control over the environment and resources, and you can customize the runner to meet your specific requirements. This makes self-hosted runners ideal for private projects, enterprise organizations, and projects that require specific dependencies or software versions.

# **📍** Benefits of Self-Hosted Runner for Python Applications

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683397885016/80466a49-e2cc-4abc-9705-bc555e7ffaee.png align="center")

Here are some benefits of using self-hosted runners for Python applications:

1. Customization: You can customize the runner environment to match your application's requirements. For example, you can install specific Python versions, libraries, and tools.
    
2. Scalability: You can scale the runner resources, such as CPU, memory, and storage, to handle large and complex Python applications.
    
3. Security: You have full control over the runner's security, such as network access, firewall rules, and encryption.
    
4. On-premises resources: You can access and use on-premises resources, such as databases, storage, and services, from your runner.
    
5. Cost-effective: You can save on costs by using your existing infrastructure and resources for the runner.
    

## **🔹GitHub Repository to follow along:**

```plaintext
https://github.com/sumanprasad007/gitHub-actions-setup-for-python-app.git
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683397548447/2c838a88-ee9f-43fa-90d9-ed99f32a7a6c.png align="center")

## **🔹** Setting up a Self-Hosted Runner using EC2 Instance

To set up a self-hosted runner using an EC2 instance, follow these steps:

1. Create an Ubuntu instance with t2.micro size on AWS.
    
2. Configure inbound and outbound rules to allow SSH, HTTP, and HTTPS traffic.
    
3. Connect to the EC2 instance using SSH and run the following command to download and run the self-hosted runner:
    

```plaintext
mkdir actions-runner && cd actions-runner
curl -O -L https://github.com/actions/runner/releases/download/v2.283.2/actions-runner-linux-x64-2.283.2.tar.gz
tar xzf ./actions-runner-linux-x64-2.283.2.tar.gz
./config.sh --url https://github.com/<USERNAME>/<REPOSITORY> --token <TOKEN>
./run.sh
```

Replace `<USERNAME>` and `<REPOSITORY>` with your GitHub username and repository name, respectively. Replace `<TOKEN>` with a personal access token that has the `repo` scope.

1. In your repository, go to Settings &gt; Actions &gt; Runners and click on the "Add new runner" button.
    
2. Enter a name for the runner and select the operating system, architecture, and runtime environment that matches your EC2 instance.
    
3. Copy the registration token and paste it into the EC2 instance terminal when prompted.
    
4. Run the `./`[`run.sh`](http://run.sh) command again to start the runner service.
    

Now, your self-hosted runner is connected to your repository and ready to run workflows.

In short, we discussed the benefits of using self-hosted runners for Python applications and how to set them up using an EC2 instance. By using Configuring the self-hosted runner is relatively easy and can be done by following the below steps:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683397837049/1317a32e-ccbc-4c2c-929f-318b29409dfa.png align="center")

## **🔹** Detailed Configurations for Self-hosted Instance:

1. Create an Ubuntu Instance with t2-micro or any other suitable instance as per the requirement.
    
2. Configure inbound and outbound rules for ports 22, 80, and 443.
    
3. Connect the instance with GitHub Actions using SSH.
    
4. In the repository, go to Settings &gt; Actions &gt; Runner &gt; Add a new self-hosted runner.
    
5. Enter the required details like runner image, architecture, and other configuration details.
    
6. Run all the commands provided in the download section on your EC2 instance, which will set up all the connections using the tokens and authentication.
    

Once the self-hosted runner is set up, you can use it to run your workflows on your EC2 instance. In the workflow file, you can specify the runs-on parameter as the name of the self-hosted runner.

For example, if you have named your runner "my-runner", you can specify it in your workflow file like this:

## **🔹 Example of self-hosted runner:**

```plaintext
name: My First GitHub Actions

on: [push]

jobs:
  build:
    runs-on: self-hosted
    # runs-on: ubuntu-latest

    strategy:
      matrix:
        python-version: [3.8, 3.9]

    steps:
    - uses: actions/checkout@v3
    - name: Set up Python
      uses: actions/setup-python@v2
      with:
        python-version: ${{ matrix.python-version }}

    - name: Install dependencies
      run: |
        python -m pip install --upgrade pip
        pip install pytest

    - name: Run tests
      run: |
        cd src
        python -m pytest addition.py
```

This will ensure that your workflow runs on the self-hosted runner instead of the GitHub-hosted runner i.e. self-hosted-runner.yml.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683397847146/01b4d94a-77c1-4c8e-8f9e-a534181f5a29.png align="center")

# **📍** Interview Question related to GitHub Actions:

## **🔹**Why did you choose GitHub Actions over other CI/CD solutions like Jenkins, AWS CodePipeline, etc.?

There are several reasons why I chose GitHub Actions over other CI/CD solutions. Firstly, our project is open source in nature and GitHub is a popular platform for open source collaboration. Secondly, our organization is already using various features of GitHub like project management, security, and source code management, making it easier to use GitHub Actions. Finally, GitHub Actions provides the ability to set up our own runners, as well as the convenience of using GitHub-hosted runners for easier setup.

## **🔹** How do you manage your credentials in GitHub?

I use the secrets and variables option in GitHub to manage my credentials. This ensures that sensitive information like API keys, passwords, and other secrets are not exposed to the public.

## **🔹** How do you create CI files for GitHub Actions? Explain the steps in detail.

### **⚜** To create CI files for GitHub Actions, I follow these steps:

1. Create a new file named "main.yml" in the ".github/workflows" directory of your repository.
    
2. Specify the name of the workflow and the events that trigger the workflow.
    
3. Define the jobs and steps that should be run as part of the workflow.
    
4. Commit the changes to the repository and observe the workflow run in the Actions tab of the repository.
    

## **🔹** Compare GitHub Actions vs. Jenkins.

GitHub Actions and Jenkins are both popular CI/CD tools that can be used for building, testing, and deploying software applications. However, GitHub Actions is a newer tool and provides tighter integration with GitHub, while Jenkins is a more mature tool with a larger ecosystem of plugins and integrations. GitHub Actions also provides a more intuitive and user-friendly interface, while Jenkins requires more configuration and setup. Additionally, GitHub Actions provides the ability to set up self-hosted runners for better customization and control, while Jenkins requires the setup of additional infrastructure.

## **📍 Conclusion**

In conclusion, self-hosted runners provide a lot of flexibility and customization options for building and testing your applications. Using an EC2 instance to set up a self-hosted runner is a great way to get started with GitHub Actions. With this guide and the code snippets provided, you should be able to easily set up and use self-hosted runners for your Python applications.

# **📍 Resources:**

%[https://youtu.be/Rb2pUKdmdYo] 

#