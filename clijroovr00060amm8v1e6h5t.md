---
title: "Day 2 of #TerraWeek - Terraform Configuration Language (HCL)"
datePublished: Tue Jun 06 2023 04:14:47 GMT+0000 (Coordinated Universal Time)
cuid: clijroovr00060amm8v1e6h5t
slug: day-2-of-terraweek-terraform-configuration-language-hcl
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1685987579231/ba06ebf5-3cda-4a82-aa8c-3ba91f1e69e2.png
tags: software-development, aws, developer, devops, beginners

---

## 📍 Introduction

In this blog, we will explore the HashiCorp Configuration Language (HCL) syntax used in Terraform and learn how to write Terraform configurations using HCL syntax. We will also cover variables, data types, and expressions in HCL, as well as testing and debug your Terraform configurations.

### 🔹 HCL Syntax

HCL is a configuration language used by Terraform to define infrastructure as code. It is a simple, human-readable language that allows you to define resources and data sources in a declarative way.

### 🔹 Blocks

In HCL, resources and data sources are defined using blocks. A block is a collection of parameters and arguments that define a specific resource or data source. Here is an example of a block that defines an AWS EC2 instance:

```plaintext
resource "aws_instance" "my-aws-instance" {
  ami           = "ami-0c55b159cbgjg6c52g4"
  instance_type = "t2.micro"
}
```

In this example, **aws\_instance** is the block type, **my-aws-instance** is the block label, and **ami** and **instance\_type** are the parameters.

### 🔹 Parameters and Arguments

Parameters are the names of the attributes that define a resource or data source. Arguments are the values assigned to those attributes. In the example above, **ami** and **instance\_type** are the parameters, and **"ami-0c55b159cbgjg6c52g4"** and **"t2.micro"** are the arguments.

## 📍 Variables, Data Types, and Expressions

Variables are an important part of Terraform configurations. They allow you to define values that can be reused throughout your configuration. In HCL, variables are defined using the **variable** block.

### 🔹 Defining Variables

To define a variable, create a [**variable.tf**](http://variables.tf) file and add the following code:

```plaintext
variable "filename" {
  type = string
}
```

In this example, we are defining a variable called **filename** with a data type of **string**.

### 🔹 Using Variables

To use a variable in your Terraform configuration, you can reference it using the **${var.variable\_name}** syntax. Here is an example of how to use the **filename** variable in a [**main.tf**](http://main.tf) file:

```plaintext
resource "local_file" "example" {
  filename = "${var.filename}"
  content  = "Hello, World!"
}
```

In this example, we are creating a **local\_file** resource and using the **filename** variable as the name of the file.

### 🔹 Data Types and Expressions

HCL supports several data types, including strings, numbers, booleans, lists, and maps. You can also use expressions to manipulate data types. Here is an example of how to use expressions to concatenate two strings:

```plaintext
variable "first_name" {
  type = string
}

variable "last_name" {
  type = string
}

output "full_name" {
  value = "${var.first_name} ${var.last_name}"
}
```

In this example, we are defining two variables, **first\_name** and **last\_name**, and using an expression to concatenate them into a single string.

## 📍 Writing Terraform Configurations

Now that we have covered the basics of HCL syntax, variables, data types, and expressions, let's write a Terraform configuration using HCL syntax.

### 🔹 Adding Required Providers

The first step is to add the required providers to your configuration. For example, if you want to use the Docker provider, you can add the following code to your [**main.tf**](http://main.tf) file:

```plaintext
provider "docker" {
  host = "tcp://localhost:2375/"
}
```

In this example, we are adding the Docker provider and specifying the host URL.

### 🔹 Creating Resources

Next, we can create resources using HCL syntax. Here is an example of how to create a Docker container:

```plaintext
resource "docker_container" "example" {
  name  = "nginx"
  image = "nginx:latest"
  ports {
    internal = 80
    external = 8080
  }
}
```

In this example, we are creating a Docker container called **nginx** with the latest version of the **nginx** image and mapping port 80 to port 8080.

### 🔹 Creating Data Sources

Data sources allow you to retrieve information about existing resources. Here is an example of how to create a data source that retrieves information about an AWS EC2 instance:

```plaintext
data "aws_instance" "example" {
  instance_id = "i-0123456789abcdef0"
}
```

In this example, we are creating a data source that retrieves information about an AWS EC2 instance with the ID **i-0123456789abcdef0**.

## 📍 Testing and Debugging

Testing and debugging your Terraform configurations is an important part of the development process. Here are some tips and best practices for testing and debugging your configurations:

* Use the **terraform plan** command to preview changes before applying them.
    
* Use the **terraform apply** the command to apply changes to your infrastructure.
    
* Use the **terraform destroy** command to destroy resources created by your configuration.
    
* Use the **terraform state** command to view the current state of your infrastructure.
    
* Use the **terraform validate** command to check your configuration for syntax errors.
    
* Use the **terraform fmt** command to format your configuration for consistency.
    

## 📍 Conclusion

In this blog, we have explored the basics of HCL syntax and learned how to write Terraform configurations using HCL syntax. We have also covered variables, data types, and expressions in HCL, as well as testing and debugging your Terraform configurations. By following these guidelines, you can write efficient and effective Terraform configurations that will help you manage your infrastructure as code.

### 🔹 **Checkout GitHub Repository for projects:**

**🔗** [**github.com/sumanprasad007**](http://github.com/sumanprasad007)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685987696536/8997098f-51b8-4220-b67a-3cbaf9f0d9c0.png align="center")