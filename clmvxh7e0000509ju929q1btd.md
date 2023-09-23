---
title: "Mastering Serverless Deployment for Sample Python App 🚀"
datePublished: Sat Sep 23 2023 11:08:58 GMT+0000 (Coordinated Universal Time)
cuid: clmvxh7e0000509ju929q1btd
slug: mastering-serverless-deployment-for-sample-python-app
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1695467295464/f6a5b906-70ad-4bfc-b419-98593b115fc4.gif
tags: aws, devops, serverless, 90daysofdevops, trainwithshubham

---

## **Introduction**

Serverless computing has revolutionized the way we build and deploy applications. It offers a scalable, cost-effective, and hassle-free way to run code in the cloud without worrying about managing servers. In this blog post, we'll explore the process of deploying a serverless application, testing endpoints, checking logs, and ultimately destroying the application when it's no longer needed. 🌐

## **Serverless Deploy**

Deploying a serverless application is an exciting journey. Here's how to do it:

🛠️ **Serverless Framework**: We'll use the Serverless Framework, a popular choice for simplifying serverless deployment.

1. **Install the Serverless Framework**:
    
    * Make sure you have Node.js installed on your machine.
        
    * Install Serverless Framework globally using npm: `npm install -g serverless`.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695464801346/dd7cc5d2-447c-4ae8-a390-23a2aec4036a.png align="center")
        
2. **Set Up Your Project**:
    
    * Create a new directory for your project and navigate to it.
        
    * Run `serverless create` to create a new service with a predefined template.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695465621550/23750e43-74e5-47cd-8a01-a92310599491.png align="center")
        
3. **Write Your Code**:
    
    * Develop your serverless application code. For this example, we'll create an endpoint called '/message'.
        

## **Let's Test Our New Endpoint '/message'**

Testing your endpoints is crucial to ensure everything works as expected. Here's how you can do it:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695465368982/515e6710-a395-4e71-9bb2-9e4e1b93706a.png align="center")

🧪 **Testing**:

1. **Invoke the Function Locally**:
    
    * Use the `serverless invoke local` command to test your function locally before deploying.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695465471765/9e2b0ad0-e765-4e2b-b164-08fd5b42045e.png align="left")
        
2. **Deploy the Application**:
    
    * Run `serverless deploy` to deploy your application to the cloud.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695465568008/a4405bcd-b708-4334-861e-c624a32b064e.png align="center")
        
3. **Test the Endpoint**:
    
    * After deployment, you can test your endpoint using tools like Postman or `curl`.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695465722647/af9d471c-11d6-4ed3-ab39-3d997e6ea104.png align="center")
        

## **Checking Logs for This Endpoint**

Monitoring and debugging are essential in any application. Let's learn how to check logs:

📋 **Logging**:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695466003205/1513fa8b-3261-48e8-b4a7-5d07427bc6fc.png align="center")

1. **View Logs in Real-time**:
    
    * Use the `serverless logs -f functionName -t` command to view real-time logs for your function.
        
2. **Retrieve Historical Logs**:
    
    * To fetch historical logs, use `serverless logs -f functionName`.
        

## **Destroying the Serverless Application with a Single Command**

When your application is no longer needed, it's essential to clean up resources to avoid unnecessary costs:

🔥 **Cleanup**:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695466163550/e52cadea-f673-4f52-9587-054ad0213b23.png align="center")

1. **Remove the Application**:
    
    * Simply run `serverless remove` to destroy your serverless application.
        
2. **Confirm Deletion**:
    
    * Confirm the deletion of resources, and Serverless Framework will tear down your entire application stack.
        

## **Let's Verify Our Application Has Terminated or Not**

Ensuring that your application has been successfully terminated is the final step:

🔍 **Verification**:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695466211923/36bd5278-ce56-44bc-b42c-97b7ebd37c73.png align="center")

1. **Check AWS Console**:
    
    * Log in to your cloud provider's console (e.g., AWS) and verify that no resources related to your serverless application remain.
        
2. **Use Serverless Dashboard**:
    
    * If you're using Serverless Framework Pro, you can check the dashboard for the status of your application.
        

## **Conclusion**

Deploying serverless applications has become more accessible and efficient with tools like Serverless Framework. Testing endpoints, monitoring logs, and cleaning up resources are essential steps in managing serverless applications. By following the steps outlined in this guide, you can confidently deploy, test, and terminate your serverless applications with ease. 🌟

Embrace the serverless revolution and unlock the power of scalable, cost-effective, and hassle-free cloud computing! 🚀🔥

Happy Serverlessing! 💻👨‍💻👩‍💻

### **🔍 Checkout GitHub Repository for projects:**

**🔗** [**linktr.ee/sumanprasad007**](http://linktr.ee/sumanprasad007)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692607442282/98c6c100-886d-4894-80bc-db5df0141100.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

### **🔍 Check out my YouTube channel - Prasad Suman Mohan:**

🔗 [**youtube.com/@sumanprasad007**](http://youtube.com/@sumanprasad007)

%[https://youtu.be/rAYm2Go2TvY]