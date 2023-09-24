---
title: "Building a Serverless Node.js Application on AWS with CI/CD 🌐"
datePublished: Sun Sep 24 2023 10:07:50 GMT+0000 (Coordinated Universal Time)
cuid: clmxaqf9f000109l8g27x3vl9
slug: building-a-serverless-nodejs-application-on-aws-with-cicd
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1695550036847/733b1dff-81c5-46d8-bef6-c68daad4f7be.gif
tags: aws, developer, devops, 90daysofdevops, trainwithshubham

---

## **Introduction**

Building and deploying serverless applications can be an exhilarating experience. In this comprehensive guide, we'll walk through the process of creating an EC2 instance, installing Node.js and npm, creating a new serverless project, setting up AWS credentials, and deploying a serverless application. Additionally, we'll explore testing, monitoring, and the powerful world of CI/CD (Continuous Integration/Continuous Deployment). Let's dive right in! 🛠️👨‍💻

### **Prerequisites**

%[https://blog.prasadsuman.me/mastering-serverless-deployment-for-sample-python-app] 

Before we start, ensure you have the following prerequisites:

🔧 **EC2 Instance**:

* Access to an AWS EC2 instance to run your serverless project.
    

📦 **Node.js and npm**:

* Install Node.js version 20 and npm version 10 on your EC2 instance.
    

💼 **Serverless Framework**:

* Install the Serverless Framework globally: `npm install -g serverless`.
    

🔑 **AWS Credentials**:

* AWS access and secret keys with admin access to connect with your AWS account.
    

🔐 **Authentication Access**:

* Be prepared to provide authentication access by typing "yes" when prompted.
    

### **Creating a Serverless Project**

* ### The architecture of the project:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695549582135/d54a47c4-646e-4eaa-99cf-c80e47690239.png align="center")

Now that we have our prerequisites sorted, let's create a serverless project:

1. **Project Setup**:
    
    * ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695549116113/29afd3e0-7585-470e-9323-9ec68c32f794.png align="left")
        
        Start by creating a new serverless project using `serverless create`.
        
    * Provide the project name and application name as per your preference.
        
2. **AWS Configuration**:
    
    * Configure your AWS access and secret key when prompted.
        
3. **Authentication**:
    
    * Grant access by typing "yes" when asked.
        

### **Building the Serverless Application**

We've laid the foundation; now, let's build the architecture of our serverless application:

🏗️ **Project Architecture**:

1. **Project Cloning**:
    
    * Clone the repository for your serverless project using `git clone` [`https://github.com/LondheShubham153/aws-node-http-api-project.git`](https://github.com/LondheShubham153/aws-node-http-api-project.git).
        
2. **Change Directory**:
    
    * Navigate to the project directory using `cd aws-node-http-api-project`.
        
3. **Branch Selection**:
    
    * ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695549374581/93bd262f-d0e1-469b-ae86-602ade9e312d.png align="center")
        
        Switch to the 'dev' branch using `git checkout dev`.
        
4. **Serverless Configuration**:
    
    * Create a new project on the Serverless Framework website. Use `serverless --org=iamsuman007` to connect with your serverless.yaml file.
        
    * ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695549414419/e34c84ea-f79a-4794-a91b-e6ef9ddecff5.png align="center")
        
        Ensure that the application name matches the one defined in your serverless.yaml file.
        
5. **Automatic Service Creation**:
    
    * The framework will automatically create all the necessary services to run your application.
        
6. **Accessing the Application**:
    
    * ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695549495510/815ee1d4-7d4f-488e-81df-f2aef4626bc5.png align="center")
        
        Once the deployment is ready, access your application using the provided endpoint: [**https://xau655ee3l.execute-api.us-east-1.amazonaws.com/**](https://xau655ee3l.execute-api.us-east-1.amazonaws.com/) **& GET:** [**https://xau655ee3l.execute-api.us-east-1.amazonaws.com/**](https://xau655ee3l.execute-api.us-east-1.amazonaws.com/)**kaam**
        

### **Testing and Data Validation**

With your serverless application deployed, it's time to test and validate its functionality:

🧪 **Testing and Validation**:

1. **Data Insertion**:
    
    * Utilize the POST method to insert data into the table through your endpoint.
        
    * POST: [**https://xau655ee3l.execute-api.us-east-1.amazonaws.com/**](https://xau655ee3l.execute-api.us-east-1.amazonaws.com/)**kaam**
        
        * with Body:
            
            ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695549460527/9a6a0910-70b4-45ce-9c31-8f33845c3159.png align="center")
            
            ```json
            {
                "kaam": "making changes to the api"
            }
            ```
            
2. **Data Validation**:
    
    * Confirm that the data is available inside the DynamoDB table.
        
3. **Adding More Data**:
    
    * Add more data using the POST method and validate using GET.
        
    * ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695549513744/9066e556-a7cc-4400-94a9-c6a00231d90c.png align="center")
        
        View the insertion using **GET:** [**https://xau655ee3l.execute-api.us-east-1.amazonaws.com/**](https://xau655ee3l.execute-api.us-east-1.amazonaws.com/)**kaam**
        

### **CI/CD Pipeline**

To streamline your development process and ensure smooth deployments, set up a CI/CD pipeline:

🔄 **CI/CD Pipeline**:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695549530106/f1cdc120-527f-4cca-a653-f9c678105060.png align="center")

1. **Pipeline Creation**:
    
    * Create a CI/CD pipeline for your serverless application.
        
2. **Deployment**:
    
    * Ensure that your CI/CD pipeline is working seamlessly and successfully deploying changes.
        

## **Conclusion**

Building a serverless Node.js application on AWS with an EC2 instance and implementing CI/CD can be a rewarding experience. With the right setup and tools, you can create, deploy, and maintain powerful serverless applications with ease. 🌟

Now that you've mastered these steps, you're well-equipped to embark on your serverless journey. Happy coding and deploying! 💻🚀**🔍 Checkout GitHub Repository for projects:**

**🔗** [**linktr.ee/sumanprasad007**](http://linktr.ee/sumanprasad007)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692607442282/98c6c100-886d-4894-80bc-db5df0141100.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

### **🔍 Check out my YouTube channel - Prasad Suman Mohan:**

🔗 [**youtube.com/@sumanprasad007**](http://youtube.com/@sumanprasad007)

%[https://youtu.be/rAYm2Go2TvY]