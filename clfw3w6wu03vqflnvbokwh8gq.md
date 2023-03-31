---
title: "Comprehensive Interview questions for Terraform"
datePublished: Fri Mar 31 2023 05:30:39 GMT+0000 (Coordinated Universal Time)
cuid: clfw3w6wu03vqflnvbokwh8gq
slug: comprehensive-interview-questions-for-terraform
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1680185609143/ab752faf-3f66-4c8d-85ff-893521504267.png
tags: linux, python, developer, devops, beginners

---

# **📍 Introduction:**

In today's fast-paced digital world, Infrastructure as Code (IaC) has become an essential tool for developers and system administrators to create and manage their infrastructure using code. Terraform is a popular, cloud-independent IaC tool that works on API as a code. It provides an easy and efficient way to create, manage and version infrastructure.

So, what's the significance of Terraform over other IaC tools? Unlike other IaC tools, Terraform provides a single workflow that enables you to create, manage, and modify your infrastructure across different cloud providers, such as AWS, Azure, Google Cloud Platform, and more. Terraform's stateful approach makes it easy to manage resources across multiple cloud providers without having to worry about vendor lock-in.

Let's delve into some of the different files associated with Terraform:

## **🔹** What is IaC? Why Terraform?

Infrastructure as Code is the process of creating and managing infrastructure using code. Terraform is a popular cloud-independent IaC tool that works on API as code. It simplifies the process of creating and managing infrastructure by allowing developers to define infrastructure as code.

For instance, if you want to create a virtual machine in AWS, you can simply define it as code in Terraform. This code is executed to create and manage the virtual machine in AWS.

## **🔹** What are modules in Terraform?

Modules are a logical grouping of resources that provides reusable code to share with others or use with others. Modules make it easy to create and manage infrastructure across multiple cloud providers.

For instance, if you want to create a virtual machine, you can create a module that defines all the resources required to create the virtual machine. This module can be reused across different projects and cloud providers.

## **🔹** What is a state file in Terraform?

A state file is used to keep track of resources and their status. It maintains the state of the files and helps to analyze and change the infrastructure accordingly. Terraform uses the state file to track the changes made to the infrastructure.

The best way to store the state file is on a remote backend server like S3. Storing the state file on a remote backend server ensures that it is secure and accessible to authorized users only.

## **🔹** What are some of the most common Terraform CLI commands that you use every day?

Terraform has several CLI commands that are used frequently by developers and system administrators. Some of the most common commands include:

* Terraform init: initializes a new Terraform project
    
* Terraform plan: shows the changes that will be made to the infrastructure
    
* Terraform apply: applies the changes to the infrastructure
    
* Terraform refresh: refreshes the state file
    
* Terraform destroy: destroys the infrastructure
    

## **🔹** What is a Terraform backend?

A Terraform backend is used to store the .tfstate file. Wherever the .tfstate file is stored becomes the backend for that Terraform project.

## **🔹** What is a Terraform Remote backend?

A Terraform Remote backend is needed when working in a team using Terraform. A commonly used remote backend is S3 in AWS cloud, and it also adds a locking mechanism. This ensures that only one person can use the .tfstate file at a time to avoid conflicts or errors.

## **🔹** How do you handle secrets in Terraform?

To handle secrets in Terraform, you can use a remote backend and enforce a strict IAM role and policy to it. This ensures that only authorized persons can access it.

## **🔹**What is a Resource Graph in Terraform?

A Resource Graph is a dependency graph used by Terraform's internal service to show the outputs of the Terraform plan. It is also used during the [output.tf](http://output.tf) file.

## **🔹** What is Terraform State Locking?

Terraform State locking is used to avoid conflicting info caused because of multiple users trying to give instructions at the same time to terraform. For this, use the DynamoDB table to lock and track which user is currently using the .tfstate file.

## **🔹** What is a Tainted Terraform resource?

A tainted resource is one that has become degraded or damaged. When a resource is tainted, Terraform marks it as such in the state file, and proposes to replace it in the next plan. Tainting a resource manually using the terraform taint command flags it for destruction and recreation in the next apply cycle. A tainted resource is considered to be in a bad or undesirable state.

## **🔹** What is Terraform State Rollback?

Terraform State Rollback helps to move one step back if we accidentally created something that we didn't intend to. Using our Remote Backend .tfstate file, we can download the previous version of the state file and push it to the bucket. The bucket will take it as a new version, and the infrastructure will roll back to the previous version.

Now that we've covered some of the most commonly asked questions about Terraform, let's dive into the significance of Terraform over other Infrastructure as Code (IaC) tools and explore the different files associated with Terraform.

## **🔹** What's the significance of Terraform over other IaC tools?

Terraform is a popular and cloud-independent IaC tool that works on API as a Code. This means that Terraform can create and manage infrastructure across multiple cloud providers, including AWS, Google Cloud, and Microsoft Azure, among others. Unlike other IaC tools, Terraform offers a unified workflow and provides an intuitive way to manage infrastructure using code. Terraform also offers a declarative syntax that describes the desired state of the infrastructure, making it easier to understand and manage.

# **📍** What are the different files associated with Terraform?

Terraform uses different files to describe and manage infrastructure. Here are some of the most commonly used files:

## [**🔹**](http://🔹.tf) [.tf](http://🔹.tf) files:

These files are the main configuration files for Terraform. They define the desired state of the infrastructure and include the resources and providers needed to create and manage the infrastructure.

## **🔹** .tfstate files

These files are created by Terraform and store the current state of the infrastructure. The .tfstate files are used to track changes made to the infrastructure, and they are used by Terraform to determine what changes need to be made to bring the infrastructure to the desired state.

## **🔹** tfvars files

These files are used to define input variables that can be used within the Terraform configuration. Input variables can be used to customize the infrastructure and are a way to pass values to the configuration.

## **🔹** .tfplan files

These files are created by Terraform during the planning phase and provide a preview of the changes that will be made to the infrastructure.

# **📍** Conclusion:

Terraform is a powerful Infrastructure as Code tool that provides a unified workflow for managing infrastructure across multiple cloud providers. Terraform's declarative syntax and intuitive configuration files make it easier to manage and understand infrastructure. By using Terraform, organizations can save time and reduce errors by automating the creation and management of infrastructure. With its popularity and versatility, Terraform is an excellent choice for any organization looking to manage infrastructure efficiently and reliably.