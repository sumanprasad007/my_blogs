# 👩‍💻 Launch multiple EC2 Instances using Terraform & also manage secrets

# 📍 Introduction:

When launching instances with Terraform, you may need to pass sensitive information such as access keys, secret keys, and other API tokens to the Terraform code. To keep these secrets safe, you can store them in environment variables or in a separate file outside of your Terraform code. The AWS CLI makes it easy to manage these secrets by allowing you to store them in your local environment or in a separate file called the credentials file.

# 📍 Explanation:

Here's an example of how you can use the AWS CLI to manage your secrets and launch multiple EC2 instances with Terraform:

## 🔹 Steps to Follow:

1. Set up your AWS CLI credentials: Before you start using the AWS CLI, you'll need to set up your AWS credentials. You can do this by installing the AWS CLI, running the `aws configure` command, and enter your access key, secret key, and default region.
    
2. We are creating two files variables.tf to store all our variable values and main.tf to declare the resources and provider
    

## 🔸 File required:

### 1️⃣ variables.tf

```python
variable "aws_region" {
  type = string
  default = "us-east-1"
}

variable "instance_type" {
  type = string
  default = "t2.micro"
}

variable "instance_count" {
  type = number
  default = 2
}
```

### 2️⃣ main.tf

```python
provider "aws" {
  region = var.aws_region
}

resource "aws_instance" "ec2_instances" {
  count         = var.instance_count
  ami           = "ami-0c94855ba95c71c99"
  instance_type = var.instance_type

  tags = {
    Name = "EC2 Instance ${count.index}"
  }
}
```

In this example, [`variables.tf`](http://variables.tf) defines three variables:

* `aws_region`: The AWS region where the instances will be launched.
    
* `instance_type`: The instance type to use for the instances.
    
* `instance_count`: The number of instances to launch.
    

In [`main.tf`](http://main.tf), we declare the AWS provider, and then create an `aws_instance` resource. We use the `count` parameter to specify the number of instances we want to create, and the `ami` and `instance_type` parameters to specify the AMI and instance type to use.

We also use the `tags` parameter to give each instance a unique name based on its index in the `count` parameter.

To use these files to create the EC2 instances, you can run the following commands:

### 3️⃣ CLI Commands:

```python
terraform init
terraform plan -var 'instance_count=2'
terraform apply -var 'instance_count=2'
```

The `plan` command will show you the changes that will be made, and the `apply` command will create the instances. You can adjust the `instance_count` variable to launch more or fewer instances as needed.

# 📍 Conclusion:

In conclusion, you can use Terraform to launch multiple EC2 instances on AWS while keeping your secrets safe using the AWS CLI. You can store your AWS access key and secret key in environment variables or in a separate file called the credentials file, which can be managed using the AWS CLI. With the AWS CLI configured, you can launch multiple instances using Terraform code that specifies the instance count, instance type, AMI, and other parameters. Terraform makes it easy to manage your infrastructure as code, and the AWS CLI provides a flexible and secure way to manage your AWS secrets. Together, these tools provide a powerful and effective way to manage your AWS infrastructure.

**Image & Steps Credit Goes to**: [https://www.youtube.com/watch?v=E0j40hLwjhI&ab\_channel=CloudChamp](https://www.youtube.com/watch?v=E0j40hLwjhI&ab_channel=CloudChamp)