# Difference between Terraform and Cloud Formation with suitable examples

Terraform and CloudFormation are both infrastructure-as-code (IAC) tools that allow developers to create and manage cloud resources programmatically. While both tools serve a similar purpose, there are some key differences between them.

Terraform is an open-source IAC tool that supports multiple cloud providers and on-premises infrastructure. It uses a declarative language called HashiCorp Configuration Language (HCL) to define and manage infrastructure. Terraform maintains a state file that tracks the current state of the infrastructure and ensures that the desired state matches the current state.

For example, let's say you want to create an EC2 instance on AWS using Terraform. Here's what the code might look like:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1676957575511/3a266da6-5328-45ba-8db6-3d6b2764d44a.png align="center")

This code defines an AWS provider and creates an EC2 instance using the specified Amazon Machine Image (AMI) and instance type. It also applies a tag to the instance to identify it.

On the other hand, CloudFormation is an AWS-specific IAC tool that allows developers to create and manage AWS resources using JSON or YAML templates. CloudFormation templates define the resources and their properties, as well as the relationships between them. CloudFormation creates a stack for each template, which represents a collection of resources that are created, updated, or deleted together as a single unit.

For example, let's say you want to create an S3 bucket on AWS using CloudFormation. Here's what the code might look like:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1676957616809/d5769f5f-770c-4765-a864-7a900ce9eaf2.png align="center")

This code defines an S3 bucket resource with the specified bucket name.

In summary, Terraform is a cross-platform IAC tool that supports multiple cloud providers, while CloudFormation is an AWS-specific IAC tool that uses JSON or YAML templates to create and manage AWS resources. Both tools provide a way to automate the creation and management of cloud infrastructure, but the choice between them depends on factors such as the cloud provider being used and the specific requirements of the project.

Image Credit goes to: [https://www.clickittech.com/devops/terraform-vs-cloudformation/](https://www.clickittech.com/devops/terraform-vs-cloudformation/)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1676958176224/3719f5e3-53f5-4e75-9363-e928f628e7af.jpeg align="center")