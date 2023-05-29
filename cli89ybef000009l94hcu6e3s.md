---
title: "Building a Django Digital Clock App with CI/CD using GitHub Actions and Deploying to AWS"
datePublished: Mon May 29 2023 03:12:55 GMT+0000 (Coordinated Universal Time)
cuid: cli89ybef000009l94hcu6e3s
slug: building-a-django-digital-clock-app-with-cicd-using-github-actions-and-deploying-to-aws
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1685299080978/818939a7-30c1-4100-bbdc-9635f3c8ab31.png
tags: software-development, web-development, developer, devops, beginners

---

# **📍** Introduction:

In this tutorial, we will create a simple Django digital clock application, set up a CI/CD pipeline using GitHub Actions, and deploy the app to AWS Elastic Beanstalk. We will walk through each step, from creating the Django app to deploying it on AWS.

### **🔹** Prerequisites:

* Basic knowledge of Python and Django
    
* A GitHub account
    
* An AWS account
    

### **🔹** Step 1: Create the Django Digital Clock Application

1.1. Create a new Django project named **digital\_clock** by running the following command:

```plaintext
django-admin startproject digital_clock
```

1.2. Create a new Django app named **clock** by running the following command:

```plaintext
python manage.py startapp clock
```

1.3. In **clock/views.py**, add the following code:

```plaintext
from django.shortcuts import render
import datetime

def digital_clock(request):
    current_time = datetime.datetime.now().strftime('%H:%M:%S')
    return render(request, 'clock.html', {'time': current_time})
```

1.4. In **digital\_clock/urls.py**, add the following code:

```plaintext
from django.urls import path
from clock.views import digital_clock

urlpatterns = [
    path('', digital_clock, name='digital_clock'),
]
```

1.5. Create a new folder named **templates** inside the **clock** app directory and a new file named **clock.html** inside it. Add the following code to **clock.html**:

```plaintext
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Digital Clock</title>
</head>
<body>
    <h1>Current Time: {{ time }}</h1>
</body>
</html>
```

### **🔹** Step 2: Add Pytest Tests

2.1. Create a directory named **tests** inside the **clock** app directory and a file named **test\_views.py** inside it. Add the following code to **test\_views.py**:

```plaintext
import pytest
from django.urls import reverse
from django.test import Client
import re

@pytest.fixture
def client():
    client = Client()
    return client

def test_digital_clock(client):
    response = client.get(reverse('digital_clock'))
    assert response.status_code == 200
    assert b'Current Time:' in response.content
    assert re.search(rb'\d{2}:\d{2}:\d{2}', response.content) is not None
```

### **🔹** Step 3: Create the GitHub Actions Workflow

3.1. In your project's root directory, create a new directory named **.github** and a subdirectory named **workflows**. Inside **workflows**, create a file named **ci-cd.yml**. Add the following code to **ci-cd.yml**:

```plaintext
name: CI/CD Pipeline

on:
  push:
    branches:
      - main

jobs:
  build-and-test:
    runs-on: ubuntu-latest
    steps:
    - name: Checkout repository
      uses: actions/checkout@v2

    - name: Set up Python
      uses: actions/setup-python@v2
      with:
        python-version: 3.8

    - name: Install dependencies
      run: |
        python -m pip install --upgrade pip
        pip install -r requirements.txt

    - name: Run tests
      run: pytest

  deploy:
    needs: build-and-test
    runs-on: ubuntu-latest
    steps:
    - name: Checkout repository
      uses: actions/checkout@v2

    - name: Set up Python
      uses: actions/setup-python@v2
      with:
        python-version: 3.8

    - name: Install dependencies
      run: |
        python -m pip install --upgrade pip
        pip install -r requirements.txt

    - name: Install AWS CLI
      run: |
        sudo apt-get update
        sudo apt-get install -y awscli

    - name: Configure AWS credentials
      run: |
        aws configure set aws_access_key_id ${{ secrets.AWS_ACCESS_KEY_ID }}
        aws configure set aws_secret_access_key ${{ secrets.AWS_SECRET_ACCESS_KEY }}
        aws configure set default.region ${{ secrets.AWS_REGION }}

    - name: Deploy to AWS Elastic Beanstalk
      run: |
        eb init -p python-3.8 digital-clock --region ${{ secrets.AWS_REGION }}
        eb deploy
```

### **🔹** Step 4: Deploy to AWS Elastic Beanstalk

4.1. In the AWS Management Console, navigate to Elastic Beanstalk. 4.2. Click on "Create Application" and enter a name for your application. 4.3. Click on "Create Environment" and select "Web server environment". 4.4. Choose a platform that supports Python 3.8 and click "Create environment". 4.5. Once your environment is created, click on "Configuration" in the left-hand menu. 4.6. Under "Software", click on "Edit". 4.7. In the "WSGI path" field, enter **digital\_clock/wsgi.py**. 4.8. Click on "Apply". 4.9. In your GitHub repository, go to "Settings" &gt; "Secrets" and create three new secrets named **AWS\_ACCESS\_KEY\_ID**, **AWS\_SECRET\_ACCESS\_KEY**, and **AWS\_REGION**. 4.10. Paste your AWS access key ID, secret access key, and region into the value fields of the corresponding secrets.

# **📍** Conclusion:

Now you have successfully created a Django digital clock app, set up a CI/CD pipeline using GitHub Actions, and deployed the app to AWS Elastic Beanstalk. Whenever you push changes to your **main** branch, the workflow will automatically build, test, and deploy your Django app to AWS Elastic Beanstalk.

## **🔹 Checkout GitHub Repository for projects:**

**🔗** [**github.com/sumanprasad007**](http://github.com/sumanprasad007)

[![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685213035326/bd57902e-a38e-475d-a507-50644ea705dd.png?auto=compress,format&format=webp align="left")](https://github.com/sumanprasad007)