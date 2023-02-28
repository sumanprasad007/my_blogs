# Module.tf in Terraform along with it's sub-topics

# **📍 Introduction:**

[`module.tf`](http://module.tf) is a Terraform configuration file that is used to define reusable modules. A module is a self-contained piece of infrastructure that can be used as a building block for larger infrastructures. Modules can contain multiple resources and configurations, and can be parameterized to accept input variables.

## **🔹 module.tf Example:**

Here's an example [`module.tf`](http://module.tf) file that defines a module for creating an AWS EC2 instance:

```python
provider "aws" {
  region = var.region
}

resource "aws_instance" "example" {
  ami           = var.ami
  instance_type = var.instance_type
  tags = var.tags
}
```

This module creates an EC2 instance with the specified AMI, instance type, and tags. The `provider` block configures the AWS provider to use the specified region.

To use this module in another configuration, you would create a [`main.tf`](http://main.tf) file that references the module, like this:

```python
module "ec2_instance" {
  source = "./ec2_instance"

  region         = "us-west-2"
  ami            = "ami-0c55b159cbfafe1f0"
  instance_type  = "t2.micro"
  tags = {
    Name = "example-instance"
  }
}
```

In this example, the `module` block references the module defined in the `./ec2_instance` directory. The input variables `region`, `ami`, `instance_type`, and `tags` are passed to the module.

## **🔹 Subtopics:**

Other subtopics related to [`module.tf`](http://module.tf) include:

### **⚜** Module outputs:

In addition to input variables, modules can also define output values that can be used in other configurations. Output values are defined in the module using the `output` block, and can be referenced in the calling configuration using the `module.<module_name>.<output_name>` syntax.

### **⚜** Module sources:

Modules can be sourced from various locations, including local directories, Git repositories, and the Terraform Registry.

### **⚜** Module composition:

Modules can be composed of other modules, allowing for modular architectures that can be easily scaled and reused.

### **⚜** Module versioning:

Modules can be versioned using tags or commit hashes, allowing for reproducible builds and consistent infrastructure across environments.

### **⚜** Module testing:

Modules can be tested using automated testing frameworks, allowing for increased confidence in the functionality and correctness of the infrastructure.

### **⚜** Module organization:

To facilitate module reuse and maintainability, it is recommended to organize modules into a directory structure that reflects the desired hierarchy of the infrastructure. For example, modules related to networking could be stored in a `networking` directory, while modules related to databases could be stored in a `databases` directory.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1677590697037/d54e5b38-621e-4c00-940a-7a7e9f56f8d0.gif align="center")

# **📍 Conclusion:**

In Terraform, [`module.tf`](http://module.tf) is used to define reusable modules that can be used as building blocks for larger infrastructures. A module is a self-contained piece of infrastructure that can contain multiple resources and configurations, and can be parameterized to accept input variables. This allows for modular architectures that can be easily scaled and reused across multiple projects. [`module.tf`](http://module.tf) files define the resources and configurations within a module, while the [`main.tf`](http://main.tf) file references the module and passes in the necessary input variables. Modules can also define output values that can be used in other configurations, and can be composed of other modules for even greater flexibility. By using modules in Terraform, infrastructure can be built and managed more efficiently, with greater consistency and reproducibility.