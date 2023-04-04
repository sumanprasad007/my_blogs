---
title: "Setting up GitHub Workflow for Python Calculator Application"
datePublished: Tue Apr 04 2023 04:15:24 GMT+0000 (Coordinated Universal Time)
cuid: clg1qythz000g09i94tti0iar
slug: setting-up-github-workflow-for-python-calculator-application
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1680581078146/7d118c43-927e-44a6-bfab-ec79dcc63c1b.webp
tags: aws, python, developer, devops, beginners

---

# **📍 Introduction to GitHub Actions:**

GitHub Actions is a tool for automating software development workflows. With GitHub Actions, you can automate your software builds, tests, deployments, and much more, directly from your GitHub repository. It is a powerful tool for developers, as it allows them to automate many of the tasks that they would normally have to perform manually, freeing up time for more important work.

GitHub Actions is a fully integrated platform for software development, built into the GitHub repository hosting service. It is available to all GitHub users, and is free to use for public repositories.

## 🔹 Why and When to Use GitHub Actions

![](https://blog.kiprosh.com/content/images/2019/12/github-action.jpg align="left")

There are many reasons why you might want to use GitHub Actions. Here are a few of the most common:

1. Automate Your Workflows - GitHub Actions allows you to automate many of the tasks that you would normally have to perform manually, such as building and testing your code, deploying your applications, and more. This can save you a lot of time and effort, and make your development process more efficient.
    
2. Improve Your Code Quality - By automating your code builds and tests, you can catch errors and issues earlier in the development process, before they become more serious problems. This can help you to improve the overall quality of your code.
    
3. Streamline Your Collaboration - GitHub Actions makes it easy to collaborate with other developers on your team, as you can set up workflows that automatically notify other team members of changes, updates, and other important events.
    
4. Increase Your Productivity - With GitHub Actions, you can automate many of the routine tasks that you would normally have to perform manually, allowing you to focus on more important work.
    

## 🔹 GitHub Actions vs Jenkins

Jenkins is another popular tool for automating software development workflows. However, there are some key differences between Jenkins and GitHub Actions.

One of the main differences is that Jenkins is a standalone tool, while GitHub Actions is fully integrated into the GitHub platform. This means that if you are already using GitHub for your repository hosting and version control, it may be more convenient to use GitHub Actions, as you will not need to set up a separate tool.

Another difference is that Jenkins requires you to set up and manage your own build server, while GitHub Actions provides built-in support for running your workflows on GitHub-hosted virtual machines or on your own self-hosted runners. This can make it easier to get started with GitHub Actions, as you do not need to set up and manage your own infrastructure.

Finally, Jenkins is a more mature tool than GitHub Actions, with a large community of users and plugins. However, GitHub Actions is rapidly gaining popularity, and is quickly becoming a popular choice for developers.

## 🔹 Projects with Examples

Here are a few examples of projects that you can build using GitHub Actions:

1. Continuous Integration and Deployment - Set up a workflow that automatically builds and tests your code, and deploys it to your production environment when the tests pass.
    
2. Code Quality Checks - Set up a workflow that runs code quality checks on your code, such as linting and static analysis, to catch errors and improve the overall quality of your code.
    
3. Notifications - Set up a workflow that automatically sends notifications to your team when changes are made to your code, such as pull requests or issues.
    
4. Release Management - Set up a workflow that automatically creates and publishes releases of your software, including changelogs and version tagging.
    

# **📍 Setup Python App using GitHub Actions:**

Here are the steps to set up a Python calculator application with GitHub Workflow:

1. Create a new repository for your project on GitHub.
    
2. Clone the repository to your local machine.
    
3. Create a Python virtual environment for your project. You can use the following commands:
    

```python
python3 -m venv env
source env/bin/activate
```

1. Install the required packages for your project. For example, if you are using Flask, you can use the following command:
    

```python
pip install flask
```

1. Create a Python script for your calculator application. You can use any editor of your choice. Here's an example script:
    

```python
from flask import Flask, request

app = Flask(__name__)

@app.route('/')
def home():
    return 'Hello, World!'

@app.route('/add')
def add():
    a = int(request.args.get('a'))
    b = int(request.args.get('b'))
    result = a + b
    return f'{a} + {b} = {result}'

if __name__ == '__main__':
    app.run()
```

This script defines a Flask application with two routes: the home route `/` and an addition route `/add` that takes two query parameters `a` and `b`.

1. Test your application locally by running the command:
    

```python
FLASK_APP=app.py flask run
```

1. Commit your changes and push them to the repository on GitHub.
    
2. Create a new file in the `.github/workflows` directory of your repository named `python-app.yml`. Here's an example of what the contents of this file could look like:
    

```python
name: Python Application

on:
  push:
    branches: [ main ]

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Set up Python
        uses: actions/setup-python@v2
        with:
          python-version: '3.8'
      - name: Install dependencies
        run: |
          python -m pip install --upgrade pip
          pip install -r requirements.txt
      - name: Test
        run: |
          pytest tests/
      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./app.py
```

This workflow sets up a job to build and deploy your Python application. It installs Python 3.8, installs the dependencies from `requirements.txt`, runs your tests, and then deploys the app using the `peaceiris/actions-gh-pages` action.

1. Commit and push the workflow file to the repository.
    

After these steps, your Python calculator application will be automatically deployed to GitHub Pages when you push changes to the `main` branch of the repository. You can access the deployed app at `https://[your-github-username].`[`github.io/[your-repository-name]/app.py`](http://github.io/[your-repository-name]/app.py).

## 🔹 Configure Your Own Runner

If you need more control over the environment that your workflows run in, you can set up your own self-hosted runner. This allows you to use your own hardware and software to run your workflows, giving you more flexibility and control.

To set up a self-hosted runner, you will need to install and configure the GitHub Actions runner software on a machine that you control. This can be done using the following steps:

## 🔹 Steps:

1. Download the GitHub Actions Runner - You can download the runner software from the GitHub website.
    
2. Install the Runner Software - Once you have downloaded the runner software, you will need to install it on the machine that you want to use as your runner.
    
3. Register the Runner - Once you have installed the runner software, you will need to register it with your GitHub repository. This will allow you to use the runner to run your workflows.
    
4. Configure the Runner - Once you have registered your runner, you can configure it to use the environment that you want to run your workflows in. This can include things like installing dependencies, setting environment variables, and more.
    
5. Start the Runner - Once you have configured your runner, you can start it up and begin using it to run your workflows.
    

Overall, GitHub Actions is a powerful tool for automating software development workflows. With its built-in support for running workflows on GitHub-hosted virtual machines or on your own self-hosted runners, and its integration with the GitHub platform, it is a great choice for developers looking to streamline their development process and improve their productivity.

# **📍** Conclusion:

GitHub Actions is a powerful tool for automating software development workflows, with built-in support for running workflows on GitHub-hosted virtual machines or on your own self-hosted runners. By automating routine tasks, improving code quality, and streamlining collaboration, GitHub Actions can help developers save time and improve productivity. With its integration with the GitHub platform, it is a great choice for developers looking to streamline their development process.

In this Blog, we have seen how to set up a GitHub Workflow for a Python calculator application. By automating the build and deployment process, we can save time and effort and ensure that our code is always up-to-date and error-free. With the help of GitHub Actions, we can easily create custom workflows that fit the needs of our project.

# **📍 Resources:**

> ***Blogs:***
> 
> 1. [https://www.dawntraoz.com/blog/how-to-add-ci-to-frontend-project-with-github-actions/](https://www.dawntraoz.com/blog/how-to-add-ci-to-frontend-project-with-github-actions/)
>     
> 2. [https://blog.kiprosh.com/automate-deployment-with-github-actions/](https://blog.kiprosh.com/automate-deployment-with-github-actions/)
>     

```python
I invite you to check my portfolio in case you are interested in contacting me for a project!. Prasad Suman Mohan

🔵 Don't forget to follow me also on LinkedIn: https://www.linkedin.com/in/prasad-suma
```