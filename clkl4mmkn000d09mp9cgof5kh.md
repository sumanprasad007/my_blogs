---
title: "Part 2 - Terraform Scenario based Interview Questions"
datePublished: Thu Jul 27 2023 12:24:16 GMT+0000 (Coordinated Universal Time)
cuid: clkl4mmkn000d09mp9cgof5kh
slug: part-2-terraform-scenario-based-interview-questions
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1690444423867/f5bbf2a9-70df-46f4-a8c0-7945b30ff675.png
tags: interview, developer, devops, beginners, 90daysofdevops

---

# **📍 Introduction:**

This is part 2 of Terraform Secnario-based Interview Questions this blog aims to provide you with a comprehensive collection of scenario-based challenges to help you excel in your Terraform interviews. Readout part 1 of it:

%[https://blog.prasadsuman.me/terraform-interview-questions-a-guide-for-devops-engineers] 

### Scenario 5: Dynamic Resource Creation

Answer: To create multiple AWS EC2 instances dynamically based on a list of instance types, you can use Terraform's dynamic blocks and for\_each feature. For instance, suppose you have a list of instance types like \["t2.micro", "t2.small", "t2.medium"\]:

```plaintext
variable "instance_types" {
  type    = list(string)
  default = ["t2.micro", "t2.small", "t2.medium"]
}

resource "aws_instance" "ec2_instances" {
  for_each = toset(var.instance_types)

  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = each.value
}
```

When you run Terraform apply, it will create three EC2 instances with the specified instance types.

### Scenario 6: Multi-Cloud Provisioning

Answer: To provision resources across multiple cloud providers, you can define provider blocks for each cloud platform in your Terraform configuration. For example, to create an AWS EC2 instance and an Azure Virtual Machine:

```plaintext
provider "aws" {
  region = "us-east-1"
  # AWS credentials and other configuration
}

provider "azurerm" {
  features {}
  # Azure credentials and other configuration
}

resource "aws_instance" "ec2_instance" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"
  # AWS-specific configuration
}

resource "azurerm_virtual_machine" "azure_vm" {
  name                  = "example-vm"
  location              = "East US"
  resource_group_name   = "example-resource-group"
  network_interface_ids = [azurerm_network_interface.example.id]
  # Azure-specific configuration
}
```

Terraform will provision resources in both AWS and Azure based on the specified providers.

### Scenario 7: Handling Resource Failures

Answer: When a resource fails during a Terraform apply, Terraform will roll back the changes for all successfully created resources to maintain a consistent state. It's essential to handle such failures gracefully. For instance, let's say there is a failure in creating an AWS EC2 instance:

```plaintext
Error: Error creating EC2 instance: InvalidParameter: Invalid instance type
status code: 400
```

In this case, Terraform will not proceed with other resource creations, and you'll need to correct the instance type in your configuration and run `terraform apply` again.

### Scenario 8: Immutable Infrastructure

Answer: To implement immutable infrastructure with Terraform, you should avoid directly modifying running instances. Instead, you create new instances with updated configurations and then replace the existing ones. For example, when updating an AWS EC2 instance:

```plaintext
resource "aws_instance" "ec2_instance" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"
}

# To update the instance type, create a new instance with the updated configuration
resource "aws_instance" "updated_ec2_instance" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.small"
}

# Perform a blue-green deployment by switching the Elastic IP to the new instance
resource "aws_eip_association" "eip_assoc" {
  instance_id   = aws_instance.updated_ec2_instance.id
  ip            = aws_instance.updated_ec2_instance.public_ip
}

# Destroy the old instance to maintain immutable infrastructure
resource "aws_instance" "ec2_instance" {
  count = 0
}
```

This approach ensures that no changes are made to the original instance, and the updated configuration is applied to a new instance.

### Scenario 9: Versioning and Rollbacks

Answer: To version Terraform configurations and enable rollbacks, you can use a version control system like Git. Each change to the Terraform configuration should be committed and tagged appropriately. For example, using Git to manage Terraform configurations:

* Commit 1: Initial configuration of AWS EC2 instance
    
* Commit 2: Updated instance type
    
* Commit 3: Added additional security group rules
    
* Commit 4: Updated instance type again
    
* ...
    

If you need to rollback to Commit 2, you can use Git to reset the state to that specific version and then run `terraform apply`.

### Scenario 10: Large-Scale Infrastructure Management

Answer: To manage large-scale infrastructure with Terraform, you can use Terraform modules to modularize and organize your code better. For example, consider a scenario where you have multiple services, each with its set of resources:

```plaintext
project/
├── main.tf
├── variables.tf
├── outputs.tf
├── modules/
│   ├── web_service/
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   ├── outputs.tf
│   ├── db_service/
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   ├── outputs.tf
└── ...
```

By organizing your infrastructure into modules, it becomes easier to manage, update, and understand the large-scale configuration.

### Scenario 11: Infrastructure Drift Detection

Answer: To detect infrastructure drift, you can use the Terraform `terraform plan` command regularly. If there are changes made outside of Terraform, the plan will show the differences between the current state and the desired state defined in the Terraform configuration. For example, if an AWS EC2 instance was manually terminated:

```plaintext
# Output when running terraform plan
An execution plan has been generated and is shown below.
~ module.ec2_instance.aws_instance.example
    instance_state: "running" => "terminated"
```

Terraform will identify the drift and provide options to update the configuration to match the current state or apply the planned changes to revert the drift.

### Scenario 12: Terraform Cloud Remote Execution

Answer: Terraform Cloud provides a remote backend that allows collaboration among team members. Multiple users can work on the same Terraform codebase, and Terraform Cloud ensures state locking to prevent concurrency issues. Version control integration with Terraform Cloud allows easy management of configurations and supports CI/CD pipelines for automated runs.

### Scenario 13: Blue-Green Deployments

Answer: To implement blue-green deployments using Terraform, you can set up a separate set of infrastructure (blue) alongside the existing one (green). Once the blue infrastructure is ready, you switch the traffic from green to blue. Here's an example using AWS Elastic Beanstalk for a web application:

```plaintext
resource "aws_elastic_beanstalk_environment" "blue_environment" {
  name                = "my-app-blue"
  solution_stack_name = "64bit Amazon Linux 2 v5.4.2 running PHP 7.4"
}

# Deploy application to the blue environment

resource "aws_elastic_beanstalk_environment" "green_environment" {
  name                = "my-app-green"
  solution_stack_name = "64bit Amazon Linux 2 v5.4.2 running PHP 7.4"
}

# Route traffic from green to blue
resource "aws_route53_record" "app_cname" {
  name    = "my-app.example.com"
  type    = "CNAME"
  records = [aws_elastic_beanstalk_environment.blue_environment.cname]
  zone_id = "your_route53_zone_id"
}

resource "aws_elastic_beanstalk_environment" "green_environment" {
  count = 0
}
```

In this example, traffic is initially directed to the green environment, and once the blue environment is ready, it's switched to blue by updating the DNS record.

### Scenario 14: Infrastructure as Code Reviews

Answer: Conducting code reviews for Terraform configurations involves analyzing the configuration code for readability, efficiency, security, and adherence to best practices. Ensure the code is well-structured, follows naming conventions, and uses appropriate variable definitions. Check for potential security issues, such as hard-coded secrets, and recommend using Terraform variables or external secret management tools. Use linters and static analysis tools like Terraform fmt and TFLint to automate the code review process and catch common issues.

### Scenario 15: Cost Optimization

Answer: To optimize cloud costs using Terraform, you can implement dynamic scaling of resources based on usage patterns. For example, for AWS EC2 instances, you can use AWS Auto Scaling Groups to automatically adjust the number of instances based on CPU utilization or other metrics. This ensures that you have enough instances to handle the load during peak times and automatically scales down during periods of low demand. By optimizing resource usage, you can save on unnecessary infrastructure costs.

Remember, providing real-life examples and experiences during interviews demonstrates your practical understanding of Terraform and how you have applied it to real-world scenarios. It showcases your ability to use Terraform effectively in a professional environment. Good luck with your interviews!

### **🔍 Checkout GitHub Repository for projects:**

**🔗** [**github.com/sumanprasad007**](http://github.com/sumanprasad007)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689575367342/b8274e1e-eef6-4cdb-9cf6-9a66ba1c9c15.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

### **🔍 Check out my YouTube channel - Prasad Suman Mohan:**

%[https://www.youtube.com/watch?v=DRG7nBrjJ_Y&t=28s]