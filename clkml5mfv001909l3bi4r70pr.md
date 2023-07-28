---
title: "Part 3 - Terraform Scenario based Interview Questions"
datePublished: Fri Jul 28 2023 12:54:42 GMT+0000 (Coordinated Universal Time)
cuid: clkml5mfv001909l3bi4r70pr
slug: part-3-terraform-scenario-based-interview-questions
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1690444430285/e9d49d04-b2d0-4db1-b20f-ad4ae2084fc6.png
tags: developer, devops, beginners, terraform, 90daysofdevops

---

# **📍 Introduction:**

This is part 3 of Terraform Secnario-based Interview Questions this blog aims to provide you with a comprehensive collection of scenario-based challenges to help you excel in your Terraform interviews. 🔗Checkout the Part 2 of Terraform Interview Questions:

%[https://blog.prasadsuman.me/part-2-terraform-scenario-based-interview-questions] 

### Scenario 16: Cross-Environment Resource Sharing

Answer: To create an AWS S3 bucket accessible by resources across different environments, you can use Terraform workspaces and variable files. For example, assume you have three environments: dev, staging, and prod. You can define the S3 bucket in a module and use different variable files for each environment:

```plaintext
project/
├── main.tf
├── variables.tf
├── dev.tfvars
├── staging.tfvars
├── prod.tfvars
├── modules/
│   └── s3_bucket/
│       ├── main.tf
│       ├── variables.tf
│       └── outputs.tf
```

In the module configuration (`modules/s3_bucket/main.tf`), you can use a variable to define the bucket name:

```plaintext
variable "bucket_name" {}

resource "aws_s3_bucket" "bucket" {
  bucket = var.bucket_name
  # other S3 bucket configurations
}
```

Then, in the environment-specific variable files (e.g., `dev.tfvars`, `staging.tfvars`, `prod.tfvars`), you can provide the appropriate bucket names:

```plaintext
# dev.tfvars
bucket_name = "my-app-dev"

# staging.tfvars
bucket_name = "my-app-staging"

# prod.tfvars
bucket_name = "my-app-prod"
```

You can then select the appropriate environment and apply the Terraform configuration with:

```plaintext
terraform apply -var-file=dev.tfvars
```

### Scenario 17: Handling Terraform State Corruption

Answer: To recover from a corrupted or lost Terraform state, you can use a state backup and restore process. Terraform provides the `terraform state` command to manage state files. Before applying changes, you can create a backup of the current state:

```plaintext
terraform state pull > terraform_state_backup.tfstate
```

If the state becomes corrupted or lost, you can restore it using the backup:

```plaintext
mv terraform_state_backup.tfstate terraform.tfstate
```

This process ensures that you can revert to the last known state and continue managing your infrastructure from there.

### Scenario 18: Multi-Tier Application Deployment

Answer: For a multi-tier application, you can use Terraform modules to represent each tier. Let's assume a simple architecture with web servers, application servers, and a database:

```plaintext
# main.tf

module "web_servers" {
  source = "./modules/web_servers"
  count  = 2
}

module "app_servers" {
  source = "./modules/app_servers"
  count  = 3

  app_port = 8080
}

module "database" {
  source = "./modules/database"
}
```

Each module (`web_servers`, `app_servers`, `database`) will have its specific configuration for the respective tier. You can use Terraform's interpolation to establish dependencies between modules.

### Scenario 19: Conditional Resource Creation

Answer: To conditionally create resources in Terraform, you can use the `count` parameter within resource blocks based on specific conditions. For example, suppose you want to create an AWS EC2 instance only in the `staging` environment:

```plaintext
resource "aws_instance" "ec2_instance" {
  count = var.environment == "staging" ? 1 : 0

  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"
}
```

In this case, the EC2 instance will be created only when the variable `environment` is set to `staging`.

### Scenario 20: Zero-Downtime Database Schema Migration

Answer: To achieve zero-downtime database schema migration using AWS RDS, you can use Terraform to create a new Read Replica with the updated schema and then promote it to the new primary instance.

```plaintext
# Create a Read Replica with the updated schema
resource "aws_db_instance" "read_replica" {
  count             = 1
  source_db_instance_identifier = aws_db_instance.primary_instance.id
  # other configurations for the Read Replica
}

# Promote the Read Replica to become the new primary instance
resource "aws_db_instance" "primary_instance" {
  count             = 1
  instance_class    = "db.t2.small"
  # other configurations for the primary instance
}

# Update application configuration to use the new primary endpoint
data "aws_route53_zone" "selected" {
  name = "example.com."
}

resource "aws_route53_record" "db_endpoint" {
  zone_id = data.aws_route53_zone.selected.zone_id
  name    = "db.example.com."
  type    = "CNAME"
  ttl     = "300"
  records = [aws_db_instance.primary_instance.endpoint]
}
```

By following this approach, the migration process is seamless with zero downtime.

### Scenario 21: Resource Tagging Strategy

Answer: To enforce consistent resource tagging across Terraform configurations, you can use Terraform's `locals` block to define common tags that apply to all resources. For example:

```plaintext
locals {
  common_tags = {
    Owner       = "DevOps Team"
    Environment = var.environment
  }
}

resource "aws_instance" "web_server" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"
  tags          = local.common_tags
}

resource "aws_s3_bucket" "static_website" {
  bucket = "example-static-website"
  acl    = "private"
  tags   = local.common_tags
}
```

This way, all resources will have the defined common tags applied, ensuring consistent tagging throughout your infrastructure.

### Scenario 22: Remote State Collaboration

Answer: To collaborate on a single Terraform configuration using remote state, you can use a remote backend like Terraform Cloud or S3. Let's consider using Terraform Cloud:

* Set up a Terraform Cloud organization and workspace for the project.
    
* Configure the workspace to use a remote backend like S3 or Terraform Cloud's managed backend.
    
* Connect each team member to the workspace using Terraform Cloud's authentication and access control features.
    
* Team members can now collaborate and perform Terraform operations using the shared workspace, while Terraform Cloud manages the state and state locking for concurrent operations.
    

1. Scenario 23: Infrastructure Audit and Compliance Answer: To conduct infrastructure audits and validate compliance, you can use Terraform's `terraform plan` and `terraform validate` commands in conjunction with external audit tools. For example, let's consider a scenario where you have defined resource tagging standards in your organization:
    
    ```plaintext
    # resource "aws_instance" ...
    
    tags = {
      Name        = "My EC2 Instance"
      Environment = "Production"
      Application = "WebApp"
    }
    ```
    
    An external audit tool or script can check the Terraform configuration against the organization's tagging standards and raise alerts for non-compliant resources. The script can be integrated into the CI/CD pipeline to enforce compliance checks before applying changes.
    

### Scenario 24: Disaster Recovery Planning

Answer: For disaster recovery planning, you can use Terraform to create a separate recovery environment in a different region. You can replicate essential resources from the primary environment to the recovery environment. For example, consider replicating an AWS EC2 instance and an RDS database to a different region:

```plaintext
# Replicate EC2 instance
resource "aws_instance" "recovery_instance" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"
  availability_zone = "us-west-1a"
  # other configurations for the recovery instance
}

# Replicate RDS database
resource "aws_db_instance" "recovery_db" {
  instance_class  = "db.t2.small"
  availability_zone = "us-west-1a"
  # other configurations for the recovery database
}
```

By using a different region, you ensure geographic redundancy and reduce the risk of data loss during a disaster.

### Scenario 25: Resource Dependency Across Terraform Configurations

Answer: To handle cross-configuration dependencies, you can use Terraform data sources to reference resources from other configurations. For example, if you have a VPC defined in one configuration and need to reference its ID in another configuration:

```plaintext
# Configuration 1 - VPC
resource "aws_vpc" "my_vpc" {
  cidr_block = "10.0.0.0/16"
}

# Configuration 2 - Security Group
data "aws_vpc" "existing_vpc" {
  default = true
}

resource "aws_security_group" "web_sg" {
  vpc_id = data.aws_vpc.existing_vpc.id
  # other security group configurations
}
```

In this example, Configuration 2 references the existing VPC from Configuration 1 using a data source.

### Scenario 26: Custom Cloud Provider Configurations

Answer: To integrate custom cloud provider configurations into Terraform, you can develop a custom provider plugin or use an existing third-party provider. Let's consider a scenario where you need to work with a custom DNS provider:

```plaintext
project/
├── main.tf
├── variables.tf
├── outputs.tf
├── provider.tf
├── modules/
└── ...
```

In the [`provider.tf`](http://provider.tf) file, you can define the custom provider:

```plaintext
terraform {
  required_providers {
    customdns = {
      source = "your_organization/customdns"
      version = "1.0.0"
    }
  }
}

provider "customdns" {
  api_key = var.customdns_api_key
  # other custom provider configurations
}
```

You can then use this provider in your Terraform resources as needed.

### Scenario 27: Automating Daily Backup of Ephemeral Data

Answer: To automate the daily backup of ephemeral data, you can use Terraform to define an AWS Lambda function and schedule it using CloudWatch Events. For example, let's consider a scenario where you have a web application running on AWS Lambda, and you want to back up the application logs daily:

```plaintext
resource "aws_cloudwatch_event_rule" "daily_backup" {
  name        = "daily_backup_rule"
  description = "Schedule daily backup"
  schedule_expression = "rate(1 day)"
}

resource "aws_lambda_function" "backup_function" {
  filename         = "backup_function.zip"
  source_code_hash = filebase64sha256("backup_function.zip")
  role             = aws_iam_role.lambda_execution.arn
  handler          = "main"
  runtime          = "python3.9"
}

resource "aws_lambda_permission" "event_permission" {
  statement_id  = "AllowExecutionFromCloudWatch"
  action        = "lambda:InvokeFunction"
  function_name = aws_lambda_function.backup_function.function_name
  principal     = "events.amazonaws.com"
  source_arn    = aws_cloudwatch_event_rule.daily_backup.arn
}

resource "aws_cloudwatch_event_target" "target" {
  rule      = aws_cloudwatch_event_rule.daily_backup.name
  arn       = aws_lambda_function.backup_function.arn
}
```

This configuration schedules a daily backup using a Lambda function triggered by CloudWatch Events.

### Scenario 28: Multi-Region Infrastructure Deployment

Answer: To deploy resources across multiple AWS regions using Terraform, you can use Terraform workspaces or use conditional resource creation based on the selected region. For example, let's consider deploying an AWS EC2 instance in two different regions:

```plaintext
variable "aws_region" {
  default = "us-west-1"
}

resource "aws_instance" "web_server" {
  count = var.aws_region == "us-west-1" ? 1 : 0
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"
  # other configurations for the web server in us-west-1
}

resource "aws_instance" "web_server" {
  count = var.aws_region == "us-east-1" ? 1 : 0
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"
  # other configurations for the web server in us-east-1
}
```

In this example, the EC2 instance will be created in the specified AWS region.

### Scenario 29: Granular Access Control

Answer: To implement granular access control for different teams working with Terraform, you can leverage Terraform Cloud's or AWS IAM's fine-grained access policies. For example, let's consider a situation where you need to grant read-only access to a specific Terraform workspace in Terraform Cloud:

```plaintext
# In Terraform Cloud's workspace settings, add a new user API token for read-only access

terraform {
  backend "remote" {
    hostname = "app.terraform.io"
    organization = "your_organization"

    workspaces {
      name = "workspace-name"

      # Read-only access for the user's token
      token = "user-read-only-token"
    }
  }
}
```

This approach ensures that the user's token only has read permissions for the specified workspace.

### Scenario 30: Cost Estimation and Forecasting

Answer: To estimate and forecast infrastructure costs using Terraform, you can use cost estimation tools like "terraform-cost-estimation" or integrate with AWS Cost Explorer. For example, with AWS Cost Explorer integration:

```plaintext
data "aws_cost_forecast" "cost" {
  time_period {
    start = "2023-01-01"
    end   = "2023-12-31"
  }

  metric = "BLENDED_COST"
  granularity = "MONTHLY"
}

output "total_cost_2023" {
  value = data.aws_cost_forecast.cost.forecast[11] # Forecast for December 2023
}
```

This configuration fetches the estimated cost forecast for the entire year of 2023 and outputs the total cost for December 2023.

By providing real-life examples and detailed explanations, you demonstrate your practical knowledge and experience with Terraform, making you a valuable asset as a DevOps engineer. Good luck with your interviews!

### **🔍 Checkout GitHub Repository for projects:**

**🔗** [**github.com/sumanprasad007**](http://github.com/sumanprasad007)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689575367342/b8274e1e-eef6-4cdb-9cf6-9a66ba1c9c15.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

### **🔍 Check out my YouTube channel - Prasad Suman Mohan:**

%[https://youtu.be/DRG7nBrjJ_Y]