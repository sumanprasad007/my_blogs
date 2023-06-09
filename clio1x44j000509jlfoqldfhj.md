---
title: "Day 5 of #TerraWeek - Terraform Modules"
datePublished: Fri Jun 09 2023 04:12:20 GMT+0000 (Coordinated Universal Time)
cuid: clio1x44j000509jlfoqldfhj
slug: day-5-of-terraweek-terraform-modules
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1686078485210/b24531d9-ecc8-4ae8-938b-cf97c63f1400.png
tags: aws, web-development, developer, devops, beginners

---

## **📍** Introduction

In this blog post, we will explore the concept of Terraform modules, their benefits, how to create and use them, and delve into module composition and versioning.

### **🔹** Understanding Terraform Modules

Terraform modules are self-contained packages of Terraform configurations that encapsulate a set of resources and their dependencies. Modules allow you to create reusable infrastructure components that can be shared across multiple projects or environments. By using modules, you can simplify your Terraform code, improve maintainability, and promote best practices.

### **🔹** Benefits of Using Terraform Modules

Using Terraform modules offers several benefits, including:

* Code reusability: Modules enable you to create reusable infrastructure components that can be shared across multiple projects or environments, reducing code duplication and improving maintainability.
    
* Simplified code: By encapsulating complex infrastructure configurations in modules, you can simplify your Terraform code and make it easier to understand and manage.
    
* Consistency: Modules help ensure that your infrastructure is consistent across different environments, reducing the risk of configuration drift and making it easier to enforce best practices.
    
* Versioning: Terraform modules support versioning, allowing you to track changes to your modules over time and roll back to previous versions if needed.
    

### **🔹** Creating and Using Terraform Modules

To create a Terraform module, you'll need to create a new directory containing a set of **.tf** files that define the resources and variables for your module. Here's an example of a simple module that creates an AWS S3 bucket:

**modules/s3\_bucket/main.tf**:

```plaintext
resource "aws_s3_bucket" "this" {
  bucket = var.bucket_name
  acl    = var.acl
}

variable "bucket_name" {
  description = "The name of the S3 bucket"
  type        = string
}

variable "acl" {
  description = "The access control list for the S3 bucket"
  type        = string
  default     = "private"
}
```

To use this module in your Terraform configuration, you'll need to add a **module** block that references the module's directory:

[**main.tf**](http://main.tf):

```plaintext
provider "aws" {
  region = "us-west-2"
}

module "s3_bucket" {
  source      = "./modules/s3_bucket"
  bucket_name = "my-example-bucket"
}
```

### **🔹** Module Composition

Module composition refers to the practice of using one module within another module to create more complex infrastructure configurations. By composing modules, you can build modular and scalable infrastructure components that can be easily managed and updated.

Here's an example of module composition using the S3 bucket module we created earlier:

**modules/static\_website/main.tf**:

```plaintext
module "s3_bucket" {
  source      = "../s3_bucket"
  bucket_name = var.bucket_name
  acl         = "public-read"
}

resource "aws_s3_bucket_policy" "this" {
  bucket = module.s3_bucket.this.id

  policy = jsonencode({
    Version = "2012-10-17"
    Statement = [
      {
        Action   = ["s3:GetObject"]
        Effect   = "Allow"
        Resource = "${module.s3_bucket.this.arn}/*"
        Principal = "*"
      }
    ]
  })
}

variable "bucket_name" {
  description = "The name of the S3 bucket for the static website"
  type        = string
}
```

### **🔹** Module Versioning

Terraform modules support versioning, allowing you to track changes to your modules over time and roll back to previous versions if needed. To version your modules, you can use a version control system like Git and tag your module releases with semantic versioning.

To reference a specific version of a module in your Terraform configuration, you can use the **version** argument in the **module** block:

[**main.tf**](http://main.tf):

```plaintext
provider "aws" {
  region = "us-west-2"
}

module "s3_bucket" {
  source      = "git::https://example.com/your-repo.git?ref=v1.0.0"
  bucket_name = "my-example-bucket"
}
```

## **📍** Conclusion

Terraform modules are a powerful feature that enables you to create reusable infrastructure components and promote code reusability and maintainability. By understanding the concept of Terraform modules, learning how to create and use them, and exploring module composition and versioning, you can build modular and scalable infrastructure components that can be easily managed and updated. This will help you create more efficient and maintainable Terraform configurations, allowing you to focus on building and deploying your applications with confidence.

### **🔹 Checkout GitHub Repository for projects:**

**🔗** [**github.com/sumanprasad007**](http://github.com/sumanprasad007)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685987696536/8997098f-51b8-4220-b67a-3cbaf9f0d9c0.png?auto=compress,format&format=webp&auto=compress,format&format=webp align="left")