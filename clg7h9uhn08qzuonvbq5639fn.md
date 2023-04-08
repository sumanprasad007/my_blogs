---
title: "How to Host a Static Website Using S3 Bucket: A Step-by-Step Guide"
datePublished: Sat Apr 08 2023 04:30:39 GMT+0000 (Coordinated Universal Time)
cuid: clg7h9uhn08qzuonvbq5639fn
slug: how-to-host-a-static-website-using-s3-bucket-a-step-by-step-guide
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1680853969482/fb4b8e84-f088-4f79-b04e-b9aae40f4cbe.png
tags: linux, aws, developer, devops, beginners

---

# **📍 Introduction:**

Creating a static website hosting using an S3 bucket is an easy and efficient way to get your website up and running on the web. In this blog post, we will provide you with step-by-step instructions and code snippets to help you create your own static website hosting using S3.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1680853860805/d540de97-3931-4470-a4ce-83abdc169290.png align="center")

## **🔹** Step 1: Create an S3 Bucket

The first step in hosting a static website using S3 is to create a new S3 bucket in the AWS Management Console. Here's how to do it:

1. Log in to your AWS Management Console.
    
2. Click on the S3 service.
    
3. Click on the "Create Bucket" button.
    
4. Enter a unique name for your bucket and select the region you want to use.
    
5. Leave the other options as default and click on the "Create" button.
    

## **🔹** Step 2: Upload Your Website Files

Once you have created your S3 bucket, the next step is to upload your website files to the bucket. You can do this in the following way:

1. Click on your bucket name.
    
2. Click on the "Upload" button.
    
3. Select your website files and click on the "Next" button.
    
4. Leave the options as default and click on the "Upload" button.
    

## **🔹** Step 3: Enable Static Website Hosting

After uploading your website files, you need to enable static website hosting for your S3 bucket. Here's how to do it:

1. Click on your bucket name.
    
2. Click on the "Properties" button.
    
3. Click on the "Static website hosting" option.
    
4. Select the "Use this bucket to host a website" option.
    
5. Enter your index and error document names.
    
6. Click on the "Save changes" button.
    

## **🔹** Step 4: Configure Bucket Permissions

Next, you need to configure bucket permissions for your S3 bucket. Here's how to do it:

1. Click on your bucket name.
    
2. Click on the "Permissions" button.
    
3. Click on the "Bucket Policy" option.
    
4. Enter the following code snippet in the text editor:
    

```python
{
  "Version":"2012-10-17",
  "Statement":[{
    "Sid":"PublicReadGetObject",
        "Effect":"Allow",
      "Principal": "*",
      "Action":["s3:GetObject"],
      "Resource":["arn:aws:s3:::YOUR-BUCKET-NAME/*"
      ]
    }
  ]
}
```

1. Replace "YOUR-BUCKET-NAME" with your actual bucket name.
    
2. Click on the "Save changes" button.
    

## **🔹** Step 5: Test Your Website

Finally, you need to test your website to make sure it is up and running. Here's how to do it:

1. Go to the endpoint URL provided by AWS in the "Static website hosting" section.
    
2. Enter your index document name in the URL (e.g., [**http://YOUR-ENDPOINT-URL/index.html**](http://YOUR-ENDPOINT-URL/index.html)).
    
3. You should see your website up and running on the web!
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1680853806768/c89a8296-87ac-409a-a881-bdf42df1b492.png align="center")

# **📍 Conclusion:**

Hosting a static website using an S3 bucket is a simple and cost-effective way to get your website up and running on the web. With the help of the steps provided in this guide, you can easily create your own static website hosting using S3 and start sharing your content with the world.

Hashtags: #AWS #S3 #WebHosting #StaticWebsite #CloudComputing #Tutorial #HowTo #StepByStepGuide