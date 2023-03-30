---
title: "How to Set Up a Remote Backend for Terraform State File with Amazon S3"
datePublished: Thu Mar 30 2023 08:47:56 GMT+0000 (Coordinated Universal Time)
cuid: clfuvi1ok000e09kxhmkig2hz
slug: how-to-set-up-a-remote-backend-for-terraform-state-file-with-amazon-s3
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1680165379334/dbeec200-90a1-435c-8bfe-38d3187f053b.png
tags: linux, python, developer, devops, beginners

---

# **📍 Introduction:**

Terraform is a popular Infrastructure as Code (IaC) tool used to provision and manage infrastructure on cloud platforms such as AWS, Azure, and Google Cloud. Terraform uses a state file (terraform.tfstate) to keep track of the current state of your infrastructure. The state file contains all the information about the resources that Terraform has created, modified, or deleted. By default, Terraform stores the state file on the local machine where Terraform is executed. However, storing the state file on the local machine can cause issues when working in a team, where multiple people are working on the same infrastructure code. To solve this issue, Terraform provides an option to store the state file remotely.

In this blog, we will discuss how to set up a remote backend for the Terraform state file using Amazon S3 as the storage provider. We will also modify the [main.tf](http://main.tf) file to use the remote backend. Terraform provides a feature called state locking to achieve this. With state locking, Terraform uses a locking mechanism to prevent multiple users from modifying the same state file simultaneously.

To enable state locking, you need to add a DynamoDB table to your remote backend configuration. Here's an updated version of the backend configuration block that includes DynamoDB:

# **📍** Prerequisites:

Before we begin, you need to have the following prerequisites:

* An AWS account
    
* AWS CLI installed on your local machine
    
* Basic knowledge of Terraform
    

Setting up the remote backend:

## **🔹** Step 1: Create an S3 bucket

The first step is to create an S3 bucket that will be used to store the Terraform state file. You can create an S3 bucket using the AWS Management Console or AWS CLI. Here is an example of creating an S3 bucket using the AWS CLI:

```python
aws s3api create-bucket --bucket my-terraform-state-bucket --region us-west-2 --create-bucket-configuration LocationConstraint=us-west-2
```

Make sure to replace the bucket name (my-terraform-state-bucket) and region (us-west-2) with your own values.

## **🔹** Step 2: Create an S3 bucket policy

Next, we need to create an S3 bucket policy that allows Terraform to read and write to the S3 bucket. Here is an example of an S3 bucket policy:

```python
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "TerraformBucketPolicy",
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::123456789012:user/terraform-user"
      },
      "Action": [
        "s3:GetObject",
        "s3:PutObject"
      ],
      "Resource": "arn:aws:s3:::my-terraform-state-bucket/*"
    }
  ]
}
```

Make sure to replace the IAM user (terraform-user), bucket name (my-terraform-state-bucket), and AWS account ID (123456789012) with your own values.

## **🔹** Step 3: Configure the backend in [main.tf](http://main.tf)

Next, we need to modify the [main.tf](http://main.tf) file to use the remote backend. we've added a `dynamodb_table` parameter that specifies the name of the DynamoDB table to use for state locking. Note that this table needs to be created before you can use it as a state locking mechanism. Here is an example of the modified [main.tf](http://main.tf) file:

```python
terraform {
  backend "s3" {
    bucket = "my-terraform-state-bucket"
    key    = "terraform.tfstate"
    region = "us-west-2"
    dynamodb_table = "my-terraform-state-lock"
  }
}

resource "aws_dynamodb_table" "terraform_state_lock" {
  name           = "my-terraform-state-lock"
  hash_key       = "LockID"
  read_capacity  = 5
  write_capacity = 5

  attribute {
    name = "LockID"
    type = "S"
  }
}

resource "aws_instance" "example" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"
  tags = {
    Name = "example-instance"
  }
}
```

Make sure to replace the bucket name (my-terraform-state-bucket) and region (us-west-2) with your values.

## **🔹** Step 4: Initialize the backend

Finally, we need to initialize the backend by running the following command:

```python
terraform init
```

This command will download the necessary plugins and set up the remote backend.

## **🔹** Verifying the Remote Backend:

To verify that the remote backend is configured correctly, run the following command:

```python
terraform state list
```

This command will list all the resources that Terraform is managing. If the remote backend is configured correctly, you should see the resources listed without any errors.

## **🔹** Uploading State to the Remote Backend:

To upload the current state to the remote backend, run the following command:

```python
terraform state push terraform.tfstate
```

This command will upload the current state to the S3 bucket specified in the backend configuration block.

# **📍 Conclusion:**

In this blog, we discussed how to set up a remote backend for the Terraform state file using Amazon S3 as the storage provider. We also modified the [main.tf](http://main.tf) file to use the remote backend. By using a remote backend, you can collaborate with your team members on infrastructure code without worrying about the state file getting out of sync. You can also use version control to track changes to the state file over time. how to set up a remote backend for the Terraform state file using Amazon S3 as the storage provider and DynamoDB as the state locking mechanism. Here's an overview of the steps involved:

1. Create an S3 bucket to store the Terraform state file.
    
2. Modify the [main.tf](http://main.tf) file to use the S3 bucket as the backend for storing the Terraform state file.
    
3. Initialize the backend using the `terraform init` command.
    
4. Verify the remote backend configuration using the `terraform state list` command.
    
5. Create a DynamoDB table for state locking.
    
6. Modify the backend configuration in the [main.tf](http://main.tf) file to include the DynamoDB table.
    
7. Initialize the backend again using `terraform init` to enable state locking.
    

By using a remote backend with state locking, you can collaborate with your team members on infrastructure code without worrying about the state file getting out of sync. You can also use version control to track changes to the state file over time.

# **📍 Resources:**

> ***Video Resources:*** [https://youtu.be/CzdfdKWRDB8?list=PLdpzxOOAlwvIKMhk8WhzN1pYoJ1YU8Csa](https://youtu.be/CzdfdKWRDB8?list=PLdpzxOOAlwvIKMhk8WhzN1pYoJ1YU8Csa)
> 
> ***Terraform Documentation:*** [https://developer.hashicorp.com/terraform/language/settings/backends/s3](https://developer.hashicorp.com/terraform/language/settings/backends/s3)
> 
> ***Blog:*** [https://www.golinuxcloud.com/configure-s3-bucket-as-terraform-backend/](https://www.golinuxcloud.com/configure-s3-bucket-as-terraform-backend/)

```python
I invite you to check my portfolio in case you are interested in contacting me for a project!. Prasad Suman Mohan

🔵 Don't forget to follow me also on LinkedIn: https://www.linkedin.com/in/prasad-suma
```