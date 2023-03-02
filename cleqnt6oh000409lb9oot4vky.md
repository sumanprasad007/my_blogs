# Understanding the Power of output.tf for Displaying Computed Outputs

# **📍 Introduction:**

In the context of Terraform, the [`output.tf`](http://output.tf) file is used to define outputs that can be displayed after applying a Terraform configuration. Outputs are values that are computed during the Terraform run and then made available for external use, such as by other Terraform configurations or by human operators.

The [`output.tf`](http://output.tf) file must be located in the same directory as the [`main.tf`](http://main.tf) file and must define one or more `output` blocks. Each `output` block specifies a name for the output and an expression that computes the value of the output.

## **🔹 Example:**

Here is an example of an [`output.tf`](http://output.tf) file:

```python
output "instance_ip" {
  value = aws_instance.example.public_ip
}

output "instance_id" {
  value = aws_instance.example.id
}

output "instance_tags" {
  value = aws_instance.example.tags
}
```

In this example, three outputs are defined:

* `instance_ip`: This output retrieves the public IP address of an AWS EC2 instance named `example`.
    
* `instance_id`: This output retrieves the unique identifier (ID) of the same `example` instance.
    
* `instance_tags`: This output retrieves a map of tags associated with the instance.
    

Once this [`output.tf`](http://output.tf) file is applied, Terraform will display the computed output values.

## **🔹 Output Screen:**

For example:

```python
Apply complete! Resources: 1 added, 0 changed, 0 destroyed.

Outputs:

instance_id = i-0123456789abcdef
instance_ip = 203.0.113.1
instance_tags = {
  Name = "example-instance"
  Environment = "production"
}
```

These output values can then be used by other Terraform configurations or by human operators to interact with the resources managed by Terraform.

# **📍 Conclusion:**

In conclusion, [`output.tf`](http://output.tf) is a Terraform file used to define outputs that can be displayed after applying a Terraform configuration. It defines one or more `output` blocks, each specifying a name for the output and an expression that computes the value of the output. The output values can be used by other Terraform configurations or by human operators to interact with the resources managed by Terraform.