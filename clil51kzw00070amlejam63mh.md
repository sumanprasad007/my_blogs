---
title: "Day 3 of #TerraWeek - Managing Resources"
datePublished: Wed Jun 07 2023 03:16:29 GMT+0000 (Coordinated Universal Time)
cuid: clil51kzw00070amlejam63mh
slug: day-3-of-terraweek-managing-resources
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1686059012748/340e7bf1-813c-4447-986c-e1df82943cc5.png
tags: aws, web-development, developer, devops, beginners

---

## **📍** Introduction:

In this blog post, we will explore how to manage resources using Terraform, focusing on various resource types and their configurations, such as AWS EC2 instances, Azure Virtual Machines, and Google Compute Engine. We will also discuss resource dependencies, provisioners, and lifecycle management.

### **🔹** Defining and Managing Resources with Terraform

To define a resource in Terraform, you need to use the **resource** block followed by the resource type and a unique name. The resource type determines the kind of infrastructure object you want to create, while the unique name is used to reference the resource within your Terraform configuration.

Here's a basic example of a resource block:

```plaintext
resource "aws_instance" "my-ec2-instance" {
  ami           = "ami-0c94855ba95b798c7"
  instance_type = "t2.micro"
}
```

In this example, we're defining an AWS EC2 instance with the resource type **aws\_instance** and a unique name **example**. The **ami** and **instance\_type** arguments are used to configure the instance.

### **🔹** AWS EC2 Instance Configuration

```plaintext
# Define provider configuration but this is not best practice, try to use AWS CLI instead

provider "aws" {
  access_key = "<your-access-key>"
  secret_access_key = "<your-secret-access-key>"
  region = "<your-preferred-region>"
}

# Create an EC2 instance
resource "aws_instance" "my_ec2_instance" {
  ami = "<your-ami-id>"
  instance_type = "t2.micro"
  key_name = "<your-key-pair-name>"

  # Specify security group(s)
  vpc_security_group_ids = ["<your-security-group-id>"]

  # Configure networking
  subnet_id = "<your-subnet-id>"
  associate_public_ip_address = true

  # Define tags
  tags = {
    Name = "MyEC2Instance"
    Environment = "Production"
  }
}
```

Make sure to replace the placeholder values with your own information:

* `<your-access-key>` and `<your-secret-access-key>`: Your AWS access key and secret access key.
    
* `<your-preferred-region>`: The AWS region in which you want to launch the EC2 instance.
    
* `<your-ami-id>`: The ID of the Amazon Machine Image (AMI) you want to use for the instance.
    
* `<your-key-pair-name>`: The name of the key pair you want to use to SSH into the instance.
    
* `<your-security-group-id>`: The ID of the security group(s) you want to associate with the instance.
    
* `<your-subnet-id>`: The ID of the subnet in which you want to launch the instance.
    

Once you have the code ready, you can run the following Terraform commands in the directory containing the code:

```plaintext
terraform init
terraform plan
terraform apply
```

The `terraform init` command initializes the working directory, downloading the necessary provider plugins. The `terraform plan` command shows you an execution plan for the infrastructure changes. Finally, the `terraform apply` command applies the changes and creates the EC2 instance.

### **🔹** Azure Virtual Machine Configuration

To create an Azure Virtual Machine using Terraform, you need to define a resource block with the **azurerm\_virtual\_machine** resource type. Here's an example configuration:

```plaintext
resource "azurerm_virtual_machine" "my_vm" {
  name                  = "myvm"
  location              = "East US"
  resource_group_name   = "myresourcegroup"
  network_interface_ids = ["${azurerm_network_interface.my_nic.id}"]
  vm_size               = "Standard_DS1_v2"

  storage_image_reference {
    publisher = "Canonical"
    offer     = "UbuntuServer"
    sku       = "16.04-LTS"
    version   = "latest"
  }

  storage_os_disk {
    name              = "myosdisk"
    caching           = "ReadWrite"
    create_option     = "FromImage"
    managed_disk_type = "Standard_LRS"
  }

  os_profile {
    computer_name  = "myvm"
    admin_username = "ubuntu"
    admin_password = "P@ssw0rd1234!"
  }

  os_profile_linux_config {
    disable_password_authentication = false
  }
}
```

In this example, we're creating an Azure Virtual Machine with various configurations, such as the VM size, storage image reference, OS disk, and OS profile.

### **🔹** Resource Dependencies

Resource dependencies in Terraform are used to specify the order in which resources should be created, updated, or destroyed. By default, Terraform automatically detects dependencies between resources based on their configuration. However, you can also explicitly define dependencies using the **depends\_on** argument.

Here's an example of using **depends\_on** to create a dependency between an AWS EC2 instance and a security group:

```plaintext
resource "aws_security_group" "example" {
  name = "example"
}

resource "aws_instance" "example" {
  ami           = "ami-0c94855ba95b798c7"
  instance_type = "t2.micro"

  vpc_security_group_ids = ["${aws_security_group.example.id}"]

  depends_on = [aws_security_group.example]
}
```

### **🔹** Provisioners

Provisioners in Terraform are used to execute scripts or other actions on a local or remote machine as part of the resource creation or destruction process. Here's an example of using a **remote-exec** provisioner to run a script on an AWS EC2 instance:

```plaintext
resource "aws_instance" "example" {
  ami           = "ami-0c94855ba95b798c7"
  instance_type = "t2.micro"

  key_name = "my_key_pair"

  provisioner "remote-exec" {
    inline = [
      "sudo apt-get update",
      "sudo apt-get install -y nginx"
    ]
  }
}
```

In this example, the **remote-exec** provisioner runs a script to update the package index and install the Nginx web server on the EC2 instance.

### **🔹** Lifecycle Management

Terraform allows you to manage the lifecycle of resources using the **lifecycle** block. This block can be used to configure how Terraform should handle resource creation, updates, and destruction. Here's an example of using the **lifecycle** block to prevent the accidental destruction of an AWS EC2 instance:

```plaintext
resource "aws_instance" "example" {
  ami           = "ami-0c94855ba95b798c7"
  instance_type = "t2.micro"

  lifecycle {
    prevent_destroy = true
  }
}
```

In this example, the **prevent\_destroy** argument is set to **true**, which means that Terraform will not allow the EC2 instance to be destroyed.

## **📍** Conclusion:

In this blog post, we've explored how to manage resources using Terraform, focusing on various resource types and their configurations, such as AWS EC2 instances, Azure Virtual Machines, and Google Compute Engine. We've also discussed resource dependencies, provisioners, and lifecycle management. By understanding these concepts, you'll be better equipped to manage your cloud infrastructure using Terraform effectively.

### **🔹 Checkout GitHub Repository for projects:**

**🔗** [**github.com/sumanprasad007**](http://github.com/sumanprasad007)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685987696536/8997098f-51b8-4220-b67a-3cbaf9f0d9c0.png?auto=compress,format&format=webp align="left")