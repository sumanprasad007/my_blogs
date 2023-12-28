---
title: "Day 8: AWS Identity and Access Management (IAM) 🚀"
datePublished: Thu Dec 28 2023 04:00:09 GMT+0000 (Coordinated Universal Time)
cuid: clqoofimu000308lg6ayy4sjr
slug: day-8-aws-identity-and-access-management-iam
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1703696131321/c441bb8c-53f7-4b05-88bc-34e5aa44f82c.gif
tags: cloud, technology, python, web-development, kubernetes, webdev, developer, devops, terraform, web3, technical-writing-1, 90daysofdevops, trainwithshubham, 90daysofdevops-chanllenge

---

## Introduction to IAM: Users & Groups 🌐

Welcome to Day 8 of our AWS Solutions Architect journey! Today, we're exploring AWS Identity and Access Management (IAM) is a powerful global service that allows you to manage access to your AWS resources securely. Let's dive into the fundamentals, starting with users and groups:

### IAM Overview

IAM is designed to handle identity and access management on a global scale. By default, AWS provides a root account, but it's a best practice to avoid using or sharing the root account for security reasons.

### Users and Groups

* **Users:** These are individuals within your organization, each having a unique identity. Users can be organized into groups for easier management.
    
* **Groups:** Primarily a way to organize users. However, groups cannot contain other groups. A user can belong to multiple groups or none at all.
    

#### Example:

* Alice, Bob, Charles, David, and Edward are individual users.
    
* There are two groups: Developers and Operations.
    
* Additionally, there's an Audit Team, represented by Fred.
    

## Understanding IAM Permissions 🛡️

IAM's strength lies in its ability to assign permissions to users and groups through JSON-based policies. Here are the key concepts:

### Policies

* IAM policies are JSON documents specifying what actions are allowed or denied.
    
* Applying the principle of least privilege is crucial. Only grant the permissions necessary for a user or group to perform their tasks.
    

#### Example Policy:

```plaintext
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "ec2:Describe*",
      "Resource": "*"
    },
    {
      "Effect": "Allow",
      "Action": "elasticloadbalancing:Describe*",
      "Resource": "*"
    },
    {
      "Effect": "Allow",
      "Action": [
        "cloudwatch:ListMetrics",
        "cloudwatch:GetMetricStatistics",
        "cloudwatch:Describe*"
      ],
      "Resource": "*"
    }
  ]
}
```

## IAM Policies in Action 🎬

### Policies Inheritance

* Policies can be attached directly to users or groups.
    
* Users can inherit permissions from both attached policies and group memberships.
    

#### Example Diagram:

```plaintext
Alice, Bob, Charles, David, Edward
    ├── Developers (Group)
    ├── Operations (Group)
    ├── Audit Team (Group)
        ├── Fred (User)
```

### IAM Policies Structure

* Policies consist of:
    
    * **Version:** Specifies the policy language version, always include "2012-10-17."
        
    * **Id:** An optional identifier for the policy.
        
    * **Statement:** The core of the policy, comprising one or more individual statements.
        

#### Statement Structure:

* **Sid:** An optional identifier for the statement.
    
* **Effect:** Determines whether the statement allows or denies access (Allow, Deny).
    
* **Principal:** The account/user/role to which this policy applies.
    
* **Action:** A list of actions allowed or denied by the policy.
    
* **Resource:** A list of resources to which the actions apply.
    
* **Condition:** Optional conditions for when the policy is in effect.
    

## Conclusion 🚀

Understanding AWS IAM is fundamental to securing your cloud infrastructure. By grasping the concepts of users, groups, and policies, you lay the foundation for a robust and secure access management strategy. IAM's flexibility empowers you to implement the principle of least privilege effectively, ensuring your AWS resources stay secure and accessible only to those who need them. Happy IAM-ing! 🔐