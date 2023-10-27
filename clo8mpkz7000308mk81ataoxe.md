---
title: "Boto3: AWS Resources & Authentication & Authorization 🔑"
datePublished: Fri Oct 27 2023 13:08:16 GMT+0000 (Coordinated Universal Time)
cuid: clo8mpkz7000308mk81ataoxe
slug: boto3-aws-resources-authentication-authorization
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1698412062286/c99e68f0-1072-471c-be71-e7a26feb3214.gif
tags: aws, python3, devops, 90daysofdevops, trainwithshubham

---

# Introduction:

As a DevOps & Site Reliability Engineer (SRE), Boto3 is your secret weapon for managing AWS resources efficiently and ensuring robust authentication and authorization. In this guide, we'll dive into creating, managing, and deleting AWS resources, listing and describing them, and expertly handling authentication and authorization using IAM roles and policies with Boto3. 🚀

## Working with AWS Resources 🏗️

### Creating, Managing, and Deleting AWS Resources 💡

Boto3 empowers you to automate the provisioning and management of AWS resources. Let's go through some common operations:

**Creating AWS Resources**:

```plaintext
import boto3

ec2 = boto3.resource('ec2')
ec2.create_instances(ImageId='ami-12345678', MinCount=1, MaxCount=5)
```

This code creates EC2 instances with a specified Amazon Machine Image (AMI).

**Managing AWS Resources**:

```plaintext
# Modifying an S3 bucket's access control
s3 = boto3.client('s3')
s3.put_bucket_acl(Bucket='mybucket', ACL='public-read')

# Changing the size of an RDS instance
rds = boto3.client('rds')
rds.modify_db_instance(DBInstanceIdentifier='mydb', AllocatedStorage=100)
```

With Boto3, you can manage resources like S3 buckets and RDS instances effortlessly.

**Deleting AWS Resources**:

```plaintext
# Terminating an EC2 instance
ec2 = boto3.client('ec2')
ec2.terminate_instances(InstanceIds=['i-12345678'])
```

This code terminates a specific EC2 instance.

### Listing and Describing AWS Resources 📋

Boto3 makes it simple to retrieve information about your AWS resources. For instance, listing EC2 instances:

```plaintext
ec2 = boto3.client('ec2')
response = ec2.describe_instances()
instances = response['Reservations']
```

By calling `describe_instances`, you get a detailed description of your instances.

## Authentication and Authorization 🔐

### Managing IAM Roles and Policies 🛡️

**Creating an IAM Role with Boto3**:

```plaintext
import boto3

iam = boto3.client('iam')
iam.create_role(
    RoleName='MyRole',
    AssumeRolePolicyDocument={
        'Version': '2012-10-17',
        'Statement': [{
            'Effect': 'Allow',
            'Principal': {'Service': 'lambda.amazonaws.com'},
            'Action': 'sts:AssumeRole'
        }]
    }
)
```

This code creates an IAM role named 'MyRole' that can be assumed by AWS Lambda.

**Creating an IAM Policy with Boto3**:

```plaintext
iam.create_policy(
    PolicyName='MyPolicy',
    PolicyDocument={
        'Version': '2012-10-17',
        'Statement': [{
            'Effect': 'Allow',
            'Action': 's3:ListBucket',
            'Resource': 'arn:aws:s3:::mybucket'
        }]
    }
)
```

This code creates a policy named 'MyPolicy' allowing listing of objects in an S3 bucket.

### Using IAM Roles and Permissions with Boto3 💪

Once you've created IAM roles and policies, you can use them in your code:

```plaintext
import boto3
from botocore.exceptions import NoCredentialsError

try:
    # Assuming a role
    sts = boto3.client('sts')
    assumed_role = sts.assume_role(
        RoleArn='arn:aws:iam::123456789012:role/MyRole',
        RoleSessionName='MySession'
    )

    # Using assumed role credentials
    s3 = boto3.client('s3',
                      aws_access_key_id=assumed_role['Credentials']['AccessKeyId'],
                      aws_secret_access_key=assumed_role['Credentials']['SecretAccessKey'],
                      aws_session_token=assumed_role['Credentials']['SessionToken'])

    s3.list_objects(Bucket='mybucket')
except NoCredentialsError:
    print("No AWS credentials found.")
```

Here, we assume the 'MyRole' IAM role and then use its temporary credentials to access S3.

In conclusion, Boto3 equips you with the tools to efficiently manage AWS resources and implement robust authentication and authorization mechanisms with IAM roles and policies. Embrace these capabilities to supercharge your SRE tasks and ensure the reliability of your AWS infrastructure. 💪🔐

Happy automating, and may your AWS resources always be well-managed and secure! 🛡️🚀