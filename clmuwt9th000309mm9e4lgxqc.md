---
title: "Creating an AWS EKS Cluster using AWS CLI🚀"
datePublished: Fri Sep 22 2023 18:02:36 GMT+0000 (Coordinated Universal Time)
cuid: clmuwt9th000309mm9e4lgxqc
slug: creating-an-aws-eks-cluster-using-aws-cli
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1695405894911/0bd1e726-2266-4edb-92a6-d37547174201.gif
tags: aws, developer, devops, 90daysofdevops, trainwithshubham

---

# **Introduction:**

Are you ready to dive into the world of Kubernetes and take advantage of AWS Elastic Kubernetes Service (EKS)? 🤖 AWS EKS is a managed Kubernetes service that simplifies the deployment, management, and scaling of containerized applications using Kubernetes. In this step-by-step guide, we'll walk you through creating an EKS cluster from scratch, explaining each step along the way. 💡

## **Use Case: Why AWS EKS? 🤷‍♂️**

Before we dive in, let's quickly discuss why AWS EKS is a fantastic choice for managing your Kubernetes workloads:

* **Managed Service**: AWS EKS abstracts away the complexity of managing the control plane, allowing you to focus on your applications.
    
* **High Availability**: EKS offers multi-AZ clusters, ensuring your applications remain available even during AWS infrastructure failures.
    
* **Security**: EKS integrates seamlessly with AWS IAM, VPC, and other security features.
    
* **Scaling**: Effortlessly scale your clusters to meet changing demands.
    

Now, let's create our EKS cluster! 🚢

## **Step 1: Prerequisites 🛠️**

Before we begin, ensure you have:

* An AWS account 🌐
    
* AWS CLI installed and configured with necessary IAM permissions 🔑
    
* `kubectl` command-line tool installed locally 📡
    
* `eksctl` command-line tool installed locally 🛠️
    

## **Step 2: Create an IAM Role 🕴️**

We'll need an IAM role to allow EKS to manage cluster resources. Create a file named `eks-cluster-role-policy.json` with the following policy:

```plaintext
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "eks:CreateCluster",
                "eks:DescribeCluster",
                "eks:UpdateClusterConfig",
                "eks:ListClusters",
                "eks:DeleteCluster",
                "eks:TagResource",
                "eks:UntagResource"
            ],
            "Resource": "*"
        }
    ]
}
```

Then, create the IAM role:

```plaintext
aws iam create-role --role-name eks-cluster-role --assume-role-policy-document file://eks-cluster-role-policy.json
```

## **Step 3: Attach Policies to the IAM Role 🧲**

Attach the necessary policies to your IAM role for EKS and EC2:

```plaintext
aws iam attach-role-policy --policy-arn arn:aws:iam::aws:policy/AmazonEKSClusterPolicy --role-name eks-cluster-role
aws iam attach-role-policy --policy-arn arn:aws:iam::aws:policy/AmazonEKSServicePolicy --role-name eks-cluster-role
```

## **Step 4: Create the EKS Cluster 🌐**

Now, use `eksctl` to create your EKS cluster. Replace `<cluster-name>` and `<region>` with your preferred values:

```plaintext
eksctl create cluster --name <cluster-name> --region <region> --nodegroup-name standard-workers --node-type t3.medium --nodes 3 --nodes-min 1 --nodes-max 4 --node-ami auto --node-volume-size 20 --node-ssh-public-key <your-public-key>
```

This command creates a cluster with a specified node group.

## **Step 5: Configure** `kubectl` for EKS 📡

Configure `kubectl` to use your new cluster:

```plaintext
aws eks --region <region> update-kubeconfig --name <cluster-name>
```

This will update your `~/.kube/config` file.

## **Step 6: Verify Your Cluster 🧐**

Ensure your cluster is up and running:

```plaintext
kubectl get nodes
```

You should see your worker nodes in the output.

## **Step 7: Deploy Applications 🚢**

You're all set! You can now deploy your Kubernetes applications to the EKS cluster and manage them using the power of AWS EKS.

Congratulations! You've successfully created an AWS EKS cluster from scratch. You're now ready to deploy, scale, and manage containerized applications like a DevOps pro. 🎉

Happy Kubernetes-ing! 🚀🐳🌟

Remember to monitor your resources and clean up when you're done to avoid unnecessary charges. EKS allows you to focus on your applications while AWS takes care of the underlying infrastructure.

## **Step 8: Monitoring and Logging 📊📈**

Effective monitoring and logging are crucial for maintaining the health and performance of your EKS cluster. AWS provides a variety of tools for this purpose:

* **Amazon CloudWatch**: Monitor your cluster's health, resource utilization, and set up alarms for critical events.
    
* **Amazon CloudWatch Logs**: Collect logs from your containers and pods and analyze them to troubleshoot issues.
    
* **AWS CloudTrail**: Keep track of API calls and changes to your EKS cluster's configuration.
    
* **Kubernetes Dashboard**: Deploy the Kubernetes Dashboard for a visual representation of your cluster's status.
    

## **Step 9: Autoscaling 🔄**

AWS EKS makes it easy to auto-scale your applications based on demand. You can configure Horizontal Pod Autoscaling (HPA) and Cluster Autoscaler to automatically adjust the number of pods and nodes to handle varying workloads.

## **Step 10: High Availability 🏗️**

EKS offers high availability by distributing your cluster's control plane across multiple Availability Zones (AZs). Make sure your application pods are spread across nodes in different AZs for fault tolerance.

## **Step 11: Security 🔐**

* **Network Policies**: Use Kubernetes Network Policies to control traffic between pods and enhance security.
    
* **AWS Identity and Access Management (IAM)**: Fine-tune IAM roles and policies to grant permissions to pods and services.
    
* **Encryption**: Enable encryption for data at rest and in transit using AWS services like AWS Key Management Service (KMS).
    

## **Step 12: CI/CD Integration 🚢🚀**

Integrate your EKS cluster with your CI/CD pipeline for seamless application deployment. Tools like Jenkins, Travis CI, or AWS CodePipeline can help automate the process.

## **Step 13: Maintenance and Upgrades 🛠️**

Regularly update your EKS cluster to benefit from new features and security patches. AWS provides guidance on cluster upgrade processes.

## **Step 14: Cost Optimization 💰**

Keep an eye on your AWS costs by right-sizing your nodes, using spot instances for non-critical workloads, and optimizing storage.

## **Step 15: Disaster Recovery 🌪️**

Implement disaster recovery strategies, such as periodic snapshots of EBS volumes and backup strategies for your application data.

## **Conclusion 📜**

Congratulations! You've now learned how to create an AWS EKS cluster step-by-step and explored some essential considerations for managing it effectively. EKS simplifies the management of Kubernetes infrastructure, allowing you to focus on delivering applications and services.

Remember that Kubernetes and AWS EKS are continuously evolving, so stay up-to-date with the latest features and best practices. With these skills, you're well-equipped to navigate the exciting world of container orchestration and cloud-native development. Happy containerizing! 🐳🌐🚀

### **🔍 Checkout GitHub Repository for projects:**

**🔗** [**linktr.ee/sumanprasad007**](http://linktr.ee/sumanprasad007)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692607442282/98c6c100-886d-4894-80bc-db5df0141100.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

### **🔍 Check out my YouTube channel - Prasad Suman Mohan:**

🔗 [**youtube.com/@sumanprasad007**](http://youtube.com/@sumanprasad007)

%[https://youtu.be/rAYm2Go2TvY]