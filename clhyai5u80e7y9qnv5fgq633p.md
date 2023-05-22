---
title: "Step by Step Implementation of AWS Samurai - Python Project"
datePublished: Mon May 22 2023 03:30:39 GMT+0000 (Coordinated Universal Time)
cuid: clhyai5u80e7y9qnv5fgq633p
slug: step-by-step-implementation-of-aws-samurai-python-project
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1684661144051/bdea0192-4586-4cc1-bff1-72b91320ebcf.png
tags: software-development, aws, developer, devops, beginners

---

## **📍 Introduction:**

In this tutorial, we will walk through the process of implementing and executing an AWS Lambda function using a CloudWatch Event. We will convert an EBS volume from gp2 to gp3 using Python and the Boto3 library.

**Prerequisites:** Before starting this tutorial, make sure you have the following prerequisites:

1. An AWS account with appropriate permissions to create and manage Lambda functions and CloudWatch events.
    
2. Python and Boto3 library installed on your local machine for development.
    
3. An understanding of AWS Lambda and basic Python programming.
    

## **📍 High-Level Design 📐🖌️:**

Behold, a glimpse into the magnificent high-level design of AWS Samurai! The interface, adorned with the essence of our noble warrior, allows you to configure and customize the behavior of Lambda functions. Harness their power to shape the destiny of your AWS governance, ensuring optimal performance, unwavering security, and unparalleled efficiency. The screenshot presented showcases the awe-inspiring AWS Samurai interface, a portal to victory in the realm of AWS governance! 🎨👨‍💻🖥️

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684658048078/11226223-c46c-49aa-92e1-fd18ca7bc147.png?auto=compress,format&format=webp align="left")

## **🔹 Step 1: Create a new IAM role**

1. Go to the IAM service in the AWS Management Console.
    
2. Click on "Roles" in the left navigation pane.
    
3. Click "Create role".
    
4. Select "AWS service" as the trusted entity and choose "Lambda" as the service.
    
5. Attach the necessary policies for Lambda execution and EC2 volume modification.
    
6. Provide a name for the role and create it.
    
7. Attaching to Policies to the Role:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684660411829/b2c6f531-0526-4777-b0fe-448a18ea53ce.png align="center")

1. Policies for AWS Lambda:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684660551394/913a9c0e-3ca7-49e1-9169-d57e42ede95a.png align="center")

1. Policies rule for AWS EBS Volume:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684660602512/b43c291a-fb71-4487-96b3-7d8a2c308749.png align="center")

## **🔹 Step 2: Develop the Lambda function code**

1. Set up your development environment with Python and Boto3.
    
2. Create a new Python file, e.g., `lambda_function.py`.
    
3. Copy and paste the following code into the file:
    

```plaintext
import json
import boto3

    
def convert_volume_to_gp3(volume_arn):
    ec2_client = boto3.client('ec2')
    
    arn_parts = volume_arn.split(':')
    volume_id = arn_parts[-1].split('/')[-1]
    return volume_id
    
def lambda_handler(event, context):
    
    volume_arn = event['resources'][0]
    volume_id = convert_volume_to_gp3(volume_arn)
    
    ec2_client = boto3.client('ec2')
    
    response = ec2_client.modify_volume(
        VolumeId=volume_id,
        VolumeType = 'gp3',
    )
```

1. Save the file.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684660172812/a074efe7-302b-4416-9c47-6a433e302b5b.png align="center")

## **🔹 Step 3: Create a Lambda function**

1. Go to the Lambda service in the AWS Management Console.
    
2. Click "Create function".
    
3. Select "Author from scratch" as the blueprint.
    
4. Provide a name for the function and choose Python as the runtime.
    
5. Select the IAM role you created in Step 1.
    
6. Click "Create function".
    

## **🔹 Step 4: Configure the Lambda function**

1. In the function configuration page, scroll down to the "Function code" section.
    
2. Choose "Upload a .zip file" in the "Code entry type" dropdown.
    
3. Click on "Upload" and select the `lambda_function.py` file you created.
    
4. Set the "Handler" field to `lambda_function.lambda_handler`.
    
5. Set the "Timeout" according to your requirements.
    
6. Click "Save".
    

## **🔹 Step 5: Set up a CloudWatch Event**

1. Go to the CloudWatch service in the AWS Management Console.
    
2. Click on "Events" in the left navigation pane.
    
3. Click "Create rule".
    
4. Choose "Event pattern" and select the desired event source (e.g., EC2).
    
5. Configure the event pattern based on your requirements.
    
6. Select the target as "Lambda function" and choose the Lambda function you created in Step 3.
    
7. Click "Configure details".
    
8. Provide a name and description for the rule.
    
9. Click "Create rule".
    

## **🔹 Step 6: Test the Lambda function**

1. Go back to the Lambda service in the AWS Management Console.
    
2. Open the function you created in Step 3.
    
3. Click on the "Test" button in the top-right corner.
    
4. Select "Create new test event" from the dropdown.
    
5. Provide a name for the test event, e.g., "TestEvent".
    
6. Copy and paste the following JSON payload into the event body:
    

```plaintext
{
  "resources": [
    "arn:aws:ec2:region:account-id:volume/volume-id"
  ]
}
```

1. Replace `region`, `account-id`, and `volume-id` with the actual values corresponding to your AWS environment.
    
2. Click "Create".
    
3. Click on the "Test" button again to execute the Lambda function with the test event.
    
4. Monitor the execution results and check the CloudWatch logs for any error messages.
    

## **🔹 Step 7: Verify the EBS volume conversion**

1. Go to the EC2 service in the AWS Management Console.
    
2. Navigate to the volume that you specified in the test event.
    
3. Check the volume details to verify that it has been converted to gp3.
    
4. Ensure that the volume attributes (such as IOPS and throughput) meet your desired configuration.
    

**Created EBS Volume of type GP2:**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684660117514/67256c35-3df2-41be-94a3-35fdf2cdcf58.png align="center")

**Modified EBS Volume to type GP3 as per Organization Governance Compliance:**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684660144777/efcd02fc-405e-483e-a9b5-c49735068f10.png align="center")

## **📍 Conclusion:**

**In this tutorial, we covered the step-by-step process of implementing and executing an AWS Lambda function using a CloudWatch Event. We converted an EBS volume from gp2 to gp3 using Python and the Boto3 library. You can now apply this knowledge to automate various tasks and workflows using Lambda and CloudWatch in your AWS environment.**

**Remember to properly configure event patterns and IAM permissions to ensure the security and reliability of your serverless applications.**

## **📍 Resources to follow along By:**

**🔗** [**https://youtu.be/DgavixR\_w5Y**](https://youtu.be/DgavixR_w5Y)

## **🔹 Checkout GitHub Repository for projects:**

**🔗** [**github.com/sumanprasad007**](http://github.com/sumanprasad007)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684660315352/807fa765-6d69-460b-8cee-4436eb1aeb6b.png align="center")