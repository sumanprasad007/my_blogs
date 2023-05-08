---
title: "Jenkins Shared Library with Demonstration👩‍💻"
datePublished: Mon May 08 2023 04:30:39 GMT+0000 (Coordinated Universal Time)
cuid: clhechecu0cfkm0nv1zhz5stt
slug: jenkins-shared-library-with-demonstration
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1683443022407/2e0047f1-ecdc-4ca3-bebe-71a8b3c9e255.png
tags: software-development, aws, developer, devops, beginners

---

# **📍** Introduction

Jenkins is a popular open-source automation server that allows you to automate tasks such as building, testing, and deploying software. It provides a lot of flexibility in terms of customizing your pipelines, but as your Jenkins infrastructure grows, managing and maintaining your pipelines can become challenging. One way to make your Jenkins pipelines more manageable is by using shared libraries.

# **📍** Shared Libraries in Jenkins

A shared library in Jenkins is a way to store commonly used code, such as scripts or functions, that can be used by different Jenkins pipelines. Instead of writing the same code again and again in multiple pipelines, you can create a shared library and use it in all the pipelines that need it. This can make your code more organized and easier to maintain.

To use a shared library in your Jenkins pipeline, you need to define the library in your Jenkins instance. Once defined, the library can be used across all pipelines in that Jenkins instance.

# **📍** Advantages of Using Shared Libraries

1. Standardization of Pipelines: By using shared libraries, you can ensure that all your pipelines are following the same set of standards, making it easier to maintain and troubleshoot them.
    
2. Reduce Duplication of Code: Instead of writing the same code again and again in multiple pipelines, you can write it once in a shared library and reuse it across all pipelines.
    
3. Easy Onboarding of New Applications, Projects, or Teams: When a new application, project, or team is added to your Jenkins infrastructure, they can use the shared libraries, making it easier for them to get started.
    
4. One Place to Fix Issues with the Shared or Common Code: If there is an issue with the shared or common code, you can fix it in one place, and all pipelines that use that code will be updated automatically.
    
5. Code Maintenance: Shared libraries make it easier to maintain your code by reducing the amount of duplicated code and making it easier to update the code.
    
6. Reduce the Risk of Errors: By using shared libraries, you can reduce the risk of errors in your pipelines as the shared code is tested and maintained by a centralized team.
    

# **📍** Scenario-based Interview Questions on Shared Libraries

## **🔹** Can you explain what a shared library is in Jenkins, and how it can help manage your pipelines?

A shared library in Jenkins is a way to store commonly used code that can be used by different Jenkins pipelines. By using a shared library, you can reduce duplication of code, standardize pipelines, and make code maintenance easier.

## **🔹** How do you define a shared library in Jenkins, and how can you use it in your pipelines?

To define a shared library in Jenkins, you need to create a git repository that contains the shared code and define it in the Jenkins instance. Once defined, you can use the shared library in your pipelines by importing the necessary functions or scripts.To write a shared library in Jenkins, I would follow these steps:

* Create a Git repository for the shared library code.
    
* Define the library in Jenkins by specifying a name, the Git repository URL, and the default version.
    
* Write the shared library code in the Git repository.
    
* Import the shared library using the @Library annotation in a pipeline.
    
* Test the pipeline to ensure that the shared library code works correctly.
    

## **🔹** What are the advantages of using shared libraries in Jenkins?

Shared libraries in Jenkins can help with standardization of pipelines, reduce duplication of code, make it easier to onboard new applications or teams, provide a centralized place to fix issues with shared code, make code maintenance easier, and reduce the risk of errors in pipelines.

## **🔹** Handling Security Issues with Shared Libraries

When using shared libraries in Jenkins, it is essential to consider security issues. Here are some best practices for handling security issues with your Jenkins pipelines:

1. Use Credentials: If your shared library needs to access sensitive information, such as passwords or keys, use credentials in Jenkins to store them securely.
    
2. Restrict Access to Shared Libraries: Ensure that only authorized users or teams have access to your shared libraries. You can use Jenkins' built-in security features to restrict access to your shared libraries.
    
3. Review Shared Library Code: Review the code in your shared libraries regularly to ensure that it is secure and up to date. If any security vulnerabilities are found, fix them immediately.
    
4. Use Approved Libraries: Use only approved and trusted shared libraries in your Jenkins pipelines. You can create a list of approved libraries and use them exclusively in your pipelines.
    
5. Monitor Changes to Shared Libraries: Keep an eye on any changes made to your shared libraries, and investigate any unexpected changes immediately.
    
    Step by Step Demo to Write Your First Jenkins Shared Library
    

## **🔹** Step-by-step guide to writing your first Jenkins shared library:

### **⚜** Step 1:

Create a Git Repository Create a new Git repository for your shared library. This repository will contain the code for your shared library.

### **⚜** Step 2:

Define the Library in Jenkins Next, define the library in your Jenkins instance. Go to Manage Jenkins &gt; Configure System &gt; Global Pipeline Libraries. Add a new library by specifying a name, the Git repository URL, and the default version. You can also specify a retrieval method, such as Modern SCM, for retrieving the library.

### **⚜** Step 3:

Write Your Shared Library Code Write your shared library code in the Git repository you created earlier. Shared library file called `myDeployFunction.groovy`, which contains a function to deploy an application:

1. Create the `vars` directory in your shared library repository
    
2. Create a file named `myDeployFunction.groovy` inside the `vars` directory
    
3. Paste the following code inside `myDeployFunction.groovy`:
    

```plaintext
def call() {
    sh "docker build -t myapp ."
    sh "docker run -d -p 80:80 myapp"
}
```

This code will build a Docker image for your application and then run it in a container on port 80.

Once you've created and saved `myDeployFunction.groovy` in your Git repository, you can import and use it in your Jenkins pipelines using the `@Library` annotation, as shown in the step-by-step guide above.

### **⚜** Step 4:

Import Your Shared Library in a Pipeline To use your shared library in a pipeline, import it using the @Library annotation. For example:

```plaintext
@Library('my-shared-library') _

pipeline {
    agent any
    stages {
        stage('Deploy') {
            steps {
                myDeployFunction()
            }
        }
    }
}
```

In this example, we import the 'my-shared-library' library and use the myDeployFunction() function in our pipeline.

### **⚜** Step 5:

Run Your Pipeline Save and run your pipeline to test your shared library code. If everything is working correctly, you should see the output from your shared library function in the Jenkins console output.

# **📍** Conclusion

In conclusion, shared libraries in Jenkins can help you manage your pipelines more efficiently by reducing duplication of code, standardizing pipelines, and making code maintenance easier. By following best practices for handling security issues, you can use shared libraries safely and securely. We also walked through a step-by-step guide to writing your first Jenkins shared library. Start using shared libraries in your Jenkins infrastructure today to make your pipelines more manageable and efficient.