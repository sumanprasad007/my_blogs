# Understanding main.tf and variables.tf files in Terraform

# 📍 Introduction:

[`main.tf`](http://main.tf) and [`variables.tf`](http://variables.tf) are files used in Terraform, a popular infrastructure as code (IAC) tool, to define and configure infrastructure resources.

## 🔹 main.tf

[`main.tf`](http://main.tf) file: [`main.tf`](http://main.tf) is the main configuration file used in Terraform. It defines the infrastructure resources to be created, modified or deleted. The [`main.tf`](http://main.tf) file contains the resource block which describes the attributes of the resource you want to create or modify. The syntax of the resource block is as follows:

```python
resource "<provider>_<resource_type>" "<name>" {
  attribute1 = "value1"
  attribute2 = "value2"
  .
  .
  .
  attributeN = "valueN"
}
```

Here, `<provider>` is the name of the cloud service provider you are using, and `<resource_type>` is the type of resource you want to create or modify. For example, if you want to create an EC2 instance on Amazon Web Services (AWS), you would use the following syntax:

### ⚜ Example:

```python
resource "aws_instance" "example" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"
}
```

In the above example, `aws_instance` is the resource type, and `example` is the name of the resource block. The `ami` and `instance_type` attributes are specific to the EC2 instance resource type, and they define the Amazon Machine Image (AMI) and the instance type, respectively.

## 🔹 variables.tf

[`variables.tf`](http://variables.tf) file: [`variables.tf`](http://variables.tf) is a file that defines input variables for the [`main.tf`](http://main.tf) file. Input variables are used to pass information from outside of the [`main.tf`](http://main.tf) file into the resource blocks in [`main.tf`](http://main.tf). Input variables make it easy to reuse a Terraform configuration for multiple environments or scenarios. The syntax for defining a variable in [`variables.tf`](http://variables.tf) is as follows:

```python
variable "<variable_name>" {
  type        = <variable_type>
  default     = <default_value>
  description = "<description>"
}
```

Here, `<variable_name>` is the name of the variable, `<variable_type>` is the type of the variable, `<default_value>` is the default value for the variable, and `<description>` is an optional description of the variable. For example, if you want to define a variable for the region where you want to launch an EC2 instance, you would use the following syntax:

### ⚜ Example:

```python
variable "region" {
  type        = string
  default     = "us-east-1"
  description = "The AWS region where the EC2 instance should be launched"
}
```

In the above example, `region` is the name of the variable, `string` is the variable type, `"us-east-1"` is the default value, and `"The AWS region where the EC2 instance should be launched"` is the description. This variable can then be used in the [`main.tf`](http://main.tf) file like this:

### ⚜ Integration of above files:

```python
resource "aws_instance" "example" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"
  availability_zone = "${var.region}a"
}
```

In the above example, `${var.region}` is used to reference the `region` variable defined in [`variables.tf`](http://variables.tf). The availability zone for the EC2 instance is set to the value of the `region` variable

# 📍 Conclusion:

In summary, [`main.tf`](http://main.tf) is the main configuration file used in Terraform that defines the infrastructure resources to be created, modified or deleted. The `resource` block in [`main.tf`](http://main.tf) describes the attributes of the resource you want to create or modify. On the other hand, [`variables.tf`](http://variables.tf) is a file used to define input variables for the [`main.tf`](http://main.tf) file. Input variables are used to pass information from outside of the [`main.tf`](http://main.tf) file into the resource blocks in [`main.tf`](http://main.tf), making it easy to reuse a Terraform configuration for multiple environments or scenarios. By properly utilizing these two files, Terraform can efficiently create, manage and provision cloud infrastructure resources in a repeatable, consistent and reliable manner.