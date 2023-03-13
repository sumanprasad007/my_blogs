---
title: "Project:  Automating AWS Resource Tracking with Shell Scripting and AWS CLI"
seoTitle: "#AutomatedResourceTracking #ShellScripting #AWSCLI #AWSAutomation #Clo"
datePublished: Mon Mar 13 2023 12:23:09 GMT+0000 (Coordinated Universal Time)
cuid: clf6spchr00000al4fjau69xx
slug: project-automating-aws-resource-tracking-with-shell-scripting-and-aws-cli
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1678709917124/7081d924-ecff-47a7-b6c6-8e4301824d85.jpeg
tags: aws, python, developer, devops, beginners

---

# **📍 Introduction:**

In today's rapidly evolving world, organizations are constantly seeking ways to improve their operations and stay ahead of the competition. One of the ways they are doing this is by moving their operations to the cloud and automating processes. Two of the main reasons behind this shift are ease of manageability and cost efficiency. By utilizing the cloud, organizations can enjoy the flexibility of having resources available on-demand, without having to invest in costly infrastructure.

## **🔹** Using Shell Scripting to Track Resource Usage

Another way organizations can take advantage of the cloud is by tracking resource usage. This can be accomplished through the use of shell scripting, which allows users to automate tasks and monitor their resources in real-time. In this blog, we will be discussing how to use shell scripting and AWS CLI to track the status of our EC2, S3, lambda functions, and IAM every day at 6 PM.

## **🔹** Prerequisites for the Script

Before we dive into the script, there are a few prerequisites we need to have in place. First, we need to download and configure AWS CLI on our EC2 instance. Once that is done, we can proceed with creating our shell script.

## **🔹** The Script

Our shell script, which we will call "[Track-aws.sh](http://Track-aws.sh)," will utilize AWS CLI to track the status of our resources. Here's what the script looks like:

```python
#!/bin/bash
#################################################################
# Author: Prasad Suman Mohan
# Version: 1.1
# Date: 13th March, 2023
#################################################################
# Agenda: We will track - AWS S3, EC2, IAM, and Lambda Functions

# To run the script in debug mode (print the commands running to the console) 
set -x 

# list all the AWS S3
echo "Print the list of AWS S3:"
aws s3 ls
# list all the AWS EC2 instances
echo "Print the list of AWS EC2 instances:"
aws ec2 describe-instances
# list all the AWS Lambda
echo "Print the list of AWS Lambda Functions:"
aws lambda list-functions
# list all the AWS IAM users
echo "Print the list of AWS IAM users:"
aws iam list-users

# jq is used for jason data filteration-> here, we only need instance id hence we filtered out the things
# aws ec2 describe-instances | jq '.Reservations[].Instances[].InstanceId'
```

In this script, we're using AWS CLI to list all the resources for S3, EC2, Lambda functions, and IAM. We're also using the "set -x" command to run the script in debug mode, which will print the commands running to the console.

Once the script is created, we need to save it using the command ":wq!" and change the permission of the script to give it write permission to all by running "chmod +x [Track-aws.sh](http://Track-aws.sh)". Finally, we can run the script using "./[Track-aws.sh](http://Track-aws.sh)" or in file mode for readability using "./[Track-aws.sh](http://Track-aws.sh) | more".

# **📍 Conclusion:**

In conclusion, moving operations to the cloud and automating processes can provide organizations with significant benefits in terms of ease of manageability and cost efficiency. Additionally, using shell scripting and AWS CLI to track resource usage can help organizations make informed decisions and optimize their cloud operations. By following the steps outlined in this blog, you can create your own shell script to track your AWS resources and gain valuable insights into your operations.