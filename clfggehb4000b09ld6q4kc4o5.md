---
title: "Top 15 AWS Services that Every DevOps Engineers should learn"
datePublished: Mon Mar 20 2023 06:36:29 GMT+0000 (Coordinated Universal Time)
cuid: clfggehb4000b09ld6q4kc4o5
slug: top-15-aws-services-that-every-devops-engineers-should-learn
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1679229548937/aafbe6f0-0597-4f9d-81f8-0e3a0157f063.jpeg
tags: aws, python, developer, devops, beginners

---

# **📍 Introduction:**

As cloud computing continues to dominate the technology landscape, AWS has become one of the most popular cloud providers in the world. DevOps engineers play a crucial role in managing and deploying applications on AWS, and there are several key services that they should be familiar with. In this article, we'll explore the top 15 AWS services that every DevOps engineer should learn and provide examples of how they can be used.

## **📢 Services with examples:**

![Logos of the Amazon cloud services AWS on a heap on a table. Web banner format with copy space.](https://as2.ftcdn.net/v2/jpg/05/34/75/21/1000_F_534752160_FR1omD4gNaEFfrJJtKc0IMl22WYIztMV.jpg align="left")

1. **Amazon EC2:** A DevOps engineer could use EC2 to provision virtual servers for running applications in the cloud. For example, if your company wants to move a legacy application to the cloud, you could use EC2 to create virtual machines to run the application.
    
2. **Amazon S3:** S3 is great for storing and retrieving any amount of data from anywhere on the web. A DevOps engineer could use S3 to store application artifacts, such as build artifacts and release artifacts, as well as static website assets such as images and videos.
    
3. **Amazon RDS:** If your application requires a relational database, a DevOps engineer could use RDS to provision and manage a database instance. For example, you could use RDS to set up a MySQL or PostgreSQL database for your application.
    
4. **Amazon CloudWatch:** A DevOps engineer could use CloudWatch to monitor AWS resources and applications. For example, you could use CloudWatch to monitor the performance of an EC2 instance or the status of a Lambda function.
    
5. **AWS Lambda:** A DevOps engineer could use Lambda to run code without provisioning or managing servers. For example, you could use Lambda to process data from an S3 bucket or to run a serverless web application.
    
6. **AWS CodePipeline:** A DevOps engineer could use CodePipeline to automate the build, test, and deployment of code changes. For example, you could use CodePipeline to set up a continuous delivery pipeline that builds and deploys a web application to an EC2 instance.
    
7. **AWS CodeDeploy:** A DevOps engineer could use CodeDeploy to automate the deployment of applications to EC2 instances or Lambda functions. For example, you could use CodeDeploy to deploy a new version of your application to an EC2 instance.
    
8. **AWS CloudFormation:** A DevOps engineer could use CloudFormation to model and provision AWS resources. For example, you could use CloudFormation to create an entire infrastructure stack, including EC2 instances, RDS instances, and Elastic Load Balancers.
    
9. **Amazon Route 53:** A DevOps engineer could use Route 53 to route traffic to AWS services or other resources. For example, you could use Route 53 to route traffic to an EC2 instance or a load balancer.
    
10. **Amazon ECS:** A DevOps engineer could use ECS to run and scale Docker containers on AWS. For example, you could use ECS to deploy a containerized web application to a cluster of EC2 instances.
    
11. **Amazon EKS**: A DevOps engineer could use EKS to deploy, manage, and scale containerized applications using Kubernetes on AWS. For example, you could use EKS to deploy a Kubernetes cluster to run a microservices-based application.
    
12. **AWS Elastic Beanstalk:** A DevOps engineer could use Elastic Beanstalk to deploy and manage web applications on AWS. For example, you could use Elastic Beanstalk to deploy a web application that is built with Ruby on Rails or Python Flask.
    
13. **Amazon SQS:** A DevOps engineer could use SQS to decouple and scale microservices, distributed systems, and serverless applications. For example, you could use SQS to create a queue that receives messages from an S3 bucket and triggers a Lambda function to process the messages.
    
14. **Amazon SNS:** A DevOps engineer could use SNS to send and receive messages between distributed applications or services. For example, you could use SNS to notify subscribers about events that occur in your application.
    
15. **AWS IAM:** A DevOps engineer could use IAM to securely control access to AWS resources. For example, you could use IAM to create policies that allow only certain users
    

---

# **📍 AWS CLI Commands for Services:**

1. Amazon EC2:
    

```python
# Create an EC2 instance
aws ec2 run-instances --image-id ami-0c55b159cbfafe1f0 --count 1 --instance-type t2.micro --key-name my-key-pair --security-group-ids sg-12345678
```

1. Amazon S3:
    

```python
# Create an S3 bucket
aws s3api create-bucket --bucket my-bucket-name --region us-east-1
```

1. Amazon RDS:
    

```python
# Create an RDS instance
aws rds create-db-instance --db-instance-identifier mydbinstance --engine mysql --db-instance-class db.t2.micro --allocated-storage 20 --master-username mymasteruser --master-user-password mymasterpassword
```

1. Amazon CloudWatch:
    

```python
# Create a CloudWatch alarm
aws cloudwatch put-metric-alarm --alarm-name myalarm --alarm-description "My alarm description" --metric-name CPUUtilization --namespace AWS/EC2 --statistic Average --period 300 --threshold 80 --comparison-operator GreaterThanThreshold --dimensions Name=InstanceId,Value=i-12345678 --evaluation-periods 2 --alarm-actions arn:aws:sns:us-east-1:123456789012:mytopic
```

1. AWS Lambda:
    

```python
# Create a Lambda function
aws lambda create-function --function-name my-function --runtime python3.8 --role arn:aws:iam::123456789012:role/lambda-execution-role --handler index.lambda_handler --code S3Bucket=my-bucket,S3Key=my-function.zip
```

1. AWS CodePipeline:
    

```python
# Create a CodePipeline pipeline
aws codepipeline create-pipeline --pipeline-name my-pipeline --role-arn arn:aws:iam::123456789012:role/CodePipelineServiceRole --cli-input-json file://pipeline.json
```

1. AWS CodeDeploy:
    

```python
# Create a CodeDeploy application
aws deploy create-application --application-name my-app --compute-platform Server
```

1. AWS CloudFormation:
    

```python
# Create a CloudFormation stack
aws cloudformation create-stack --stack-name my-stack --template-body file://my-template.json --parameters ParameterKey=Param1,ParameterValue=value1 ParameterKey=Param2,ParameterValue=value2
```

1. Amazon Route 53:
    

```python
# Create a Route 53 record set
aws route53 change-resource-record-sets --hosted-zone-id Z123456789012 --change-batch file://record-set.json
```

1. Amazon ECS:
    

```python
# Create an ECS cluster
aws ecs create-cluster --cluster-name my-cluster
```

1. Amazon EKS:
    

```python
# Create an EKS cluster
aws eks create-cluster --name my-cluster --role-arn arn:aws:iam::123456789012:role/eks-service-role --resources-vpc-config subnetIds=subnet-12345678,subnet-23456789,securityGroupIds=sg-12345678
```

1. AWS Elastic Beanstalk:
    

```python
# Create an Elastic Beanstalk application
aws elasticbeanstalk create-application --application-name my-app
```

1. Amazon SQS:
    

```python
# Create an SQS queue
aws sqs create-queue --queue-name my-queue
```

1. Amazon SNS:
    

```python
# Create an SNS topic
aws sns create-topic --name my-topic
```

1. AWS IAM:
    

```python
# Create an IAM user
aws iam create-user --user-name my
```

---

## **🔹 Video-Link to follow along:**

%[https://youtu.be/leWJypzVyQ4?list=PLdpzxOOAlwvIKMhk8WhzN1pYoJ1YU8Csa] 

```python
I invite you to check my portfolio in case you are interested in contacting me for a project!. Prasad Suman Mohan

🔵 Don't forget to follow me also on LinkedIn: https://www.linkedin.com/in/prasad-suman-mohan/
```