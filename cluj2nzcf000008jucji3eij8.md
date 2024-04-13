---
title: "Deep Dive into Terraform - P4 (Terraform Variables)"
datePublished: Wed Apr 03 2024 00:30:51 GMT+0000 (Coordinated Universal Time)
cuid: cluj2nzcf000008jucji3eij8
slug: deep-dive-into-terraform-p4-terraform-variables
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1711865236626/863b2a6f-3546-4be2-a4d6-561db10faaf5.png
tags: cloud, aws, azure, devops, terraform, infrastructure-as-code, gcp, devsecops, 2articles1week, devops-articles, terraform-cloud, infrastructure-management, terragrunt, terraform-aws-infrastructureascode-provisioning-automation-cloudcomputing, terraform-variables

---

Before moving ahead and start discussing about the Variables in Terraform and their examples. Let's take the quick overview on the various previous aspects of Infrastructure as Code, Terraform, and Terraform State.

---

# **What is Infrastructure as Code (IaC) ?**

Terraform is an open-source infrastructure as code tool that supports multiple cloud providers and on-premises infrastructure the Infrastructure as a Code (IaC) has brought up a new approach for managing and provisioning IT infrastructure with the help of code the Infrastructure as a Code (IaC) brings automation, consistency, and scalability to infrastructure deployment and in the management of IT infrastructure. Basically, the Infrastructure as Code (IaC) is a sort of a method used in the field of cloud computing and the software development that enables the management and provision of computing infrastructure by writing and using a machine-readable script files, rather than performing the manual processes. The Infrastructure as a Code (IaC) involves the defining of various infrastructure elements such as virtual machines, networks, storage, and configurations by using code, which can be written in the declarative programming language. This code can be stored in version control systems (VCS) like Git, which will allow the teams to do collaboration, track various changes, and roll back to previous versions if necessary.

---

# **What is Terraform?**

Terraform is an open-source infrastructure as a code tool from HashiCorp. It allows users to define both on-premises and cloud resources in human-readable configuration files that can be easily versioned, reused, and shared. It transforms the way for the companies or the users to manage and deploy their infrastructure over the cloud environments. With the rise in the popularity of Terraform, it has become famous for it's efficiency, scalability, and flexibility in the world cloud computing or the cloud infrastructure environments. The terraform is not capable of managing low-level components like webservers, storage services, and networking resources but it is also capable in managing the high-level resources such as DNS, PaaS, and SaaS components. The terraform is a declarative tool which is used for simplifying the user's experience by allowing the users to specify the expected state of the resources without the need to specify the exact steps to achieve the desired state of infrastructure resources.

---

# **What is Terraform State?**

The state management in Terraform is a strategic way for maintaining infrastructure as code (IaC) effectively, efficiently and safely. The Terraform state management is a very crucial component because it stores the information about the various resources managed by the Terraform, including their configurations and dependencies. The terraform state management in crucial for its role in tracking the current state of various infrastructure deployments. The terraform uses this terraform state file for determining that what changes are needed to make to reach the desired state defined in the configuration files. The terraform state management enables the enhanced collaboration between the team members working on the same infrastructure. Storing the terraform state file in the remote backend locations. For e.g., Terraform Cloud, AWS S3, or Azure Storage the multiple team members can collaborate together and effectively on the infrastructural changes.

---

# What are Terraform Variables?

The Terraform Variables are one of the fundamental elements in the Infrastructure as Code (IaC) workflows, providing flexibility, reusability, and dynamic nature to the infrastructure configurations. The terraform variables are the kind of tools for managing infrastructure configurations in a dynamically and scalable manner, by understanding their types, patterns, and other best practices, the developers or the DevOps Engineers can use the full potential of variables to enhance their infrastructure as code (IaC) workflows, it improves the code maintainability, and can achieve great help in the management of infrastructure.

Basically, the variables in Terraform serve as placeholders for the dynamic values, by allowing for reusability and adaptability of the configurations, from defining resource attributes, configuring environments, or managing sensitive information, in every aspect the terraform variables plays a crucial role.

Terraform variables are very good in organizing the infrastructural configurations, managing environmental based settings, and securing the sensitive information. The terraform variables enables the developers or the DevOps Engineers to configure their codebases effectively and efficiently, by making them easily adoptable to the various deployment scenarios and various environments. By utilizing the best practices such as consistent name usage, documentation, and secure handling of the sensitive data, developers or the DevOps Engineers can ensure the ease and maintainability of their Terraform configurations.

## Types of Variables in Terraform

There are total three types of variables in Terraform named as:

1. Input Variables
    
2. Output Variables
    
3. Local Variables
    

### Input Variables

The Input variables in Terraform are the type of variables that can be used for values that can be passed into Terraform configurations during runtime or the execution. The Input Variables allow users to dynamically define the parameters for their infrastructure configurations, by making them reusable, flexible, and customizable as per the needs. The input variables enables the users or the developers to remove away the hard-coded values, which simply leads to the enhancement to the better Terraform code management and the organization of Terraform code at the level best. With the help of input variables, the developers or the DevOps Engineers can define defaults, constraints, and the validation rules to ensure the high consistency and reliability across the various deployments. These terraform variables play a important role in safeguarding the configuration details, by making the code more maintainable and adaptable.

For Example:- If we are provisioning a virtual machine (VM) in a cloud provider using Terraform. Instead of hard-coding specific attributes like the VM size, region, and image ID directly into the configurations, we can use the input variables to make our configurations more adaptable. So, for performing this activity of defining the Input Variables:

1. Firstly we will create a `variables.tf` file to define our input variables:
    
    ```plaintext
    variable "vm_size" {
      description = "Size of the virtual machine (For e.g., small, medium, large)"
      type        = string
    }
    
    variable "region" {
      description = "Region where you want the VM to be deployed"
      type        = string
    }
    
    variable "image_id" {
      description = "ID of the image for the VM"
      type        = string
    }
    ```
    
2. Secondly, now using the above defined input variables in the Resource Configuration for VM:
    
    ```plaintext
    resource "aws_instance" "example_vm" {
      ami           = var.image_id
      instance_type = var.vm_size
      availability_zone = var.region
    
      tags = {
        Name = "VM name"
      }
    }
    ```
    
3. Thirdly, now we will provide the input variables value's in `terraform.tfvars` file:
    
    ```plaintext
    vm_size   = "t2.medium"
    region    = "ap-south-1"
    image_id  = "ami-7887459483ewi8"
    ```
    

### Output Variables:

The Output Variables, provide a mechanism for exporting or transferring the information from Terraform configurations. The output variables allow the users to retrieve the various resource attributes and make them available for use by the external systems. Basically, the output variables provide a great way to extract the information from your deployed resources, by making it accessible for other systems, scripts, or even by other Terraform configurations. The Output variables are useful for fetching the information such as IP addresses, domain names, or other information regarding the provisioned resources using Terraform.

For Example:- We already have the terraform configurations of an AWS EC2 virtual machine in AWS cloud provider and we want to fetch the public IP address of that instance once it is deployed on AWS. So, for this activity follow the below steps for defining the output variables to fetch the Public IP address of the EC2 instance:

1. First, create the `main.tf` file for writing the AWS EC2 instance configuration:
    
    ```plaintext
    provider "aws" {
      region = "ap-south-1"
    }
    
    resource "aws_instance" "example" {
      ami           = "ami-7887459483ewi8"
      instance_type = "t2.medium"
    }
    
    output "instance_public_ip" {
      value = aws_instance.example.public_ip
    }
    ```
    
    Now, after running the `terraform apply` command and after the successfull provisioning of the EC2 instance, Terraform will throw the output of the public IP address of the EC2 instance:
    
    ```makefile
    Outputs:
    instance_public_ip = "31.14.168.300"
    ```
    

### Local Variables:

The Local variables are the variables that are used to store the intermediate values within Terraform configurations, by enhancing the organization of code and code readability. The Local variables are particularly useful for storing computed values, transforming data structures, or encapsulating conditional logic within Terraform modules. Basically, the Local variables in Terraform allow us to define values within a module that are not directly associated with specific resources and the outputs. By using local variables, we encapsulate the logic for calculating the total disk storage within the module, making the configuration more readable and maintainable

For Example:- If we have a Terraform module for provisioning a virtual machine (VM) in a cloud provider. And, you need to calculate the total amount of storage required for the virtual machine's disk based on certain parameters like the disk size and the number of disks.

```plaintext
variable "disk_size_gb" {
  description = "Size of each disk in GB"
  type        = number
}
variable "num_disks" {
  description = "Number of disks attached to the VM"
  type        = number
}

# Now, Calculating the total disk storage from here
locals {
  total_disk_storage_gb = var.disk_size_gb * var.num_disks
}
resource "example_vm" "my_vm" {
  # Other configuration settings for VM provisioning
  disk_size_gb = var.disk_size_gb
  num_disks    = var.num_disks
  total_storage_gb = local.total_disk_storage_gb
}
```

* In this, we define the two input variables `disk_size_gb` and `num_disks` to specify the size of each disk and the number of disks.
    
* Using a `locals` block, in which we calculate the `total_disk_storage_gb` by multiplying the `disk_size_gb` with the `num_disks`.
    
* The calculated `total_disk_storage_gb` is then used in the resource block `example_vm` to get the total storage in last line `total_storage_gb = local.total_disk_storage_gb` for the VM we created.
    

<mark>&lt;-- In this part of Terraform Series we discussed deeply about the Terraform Variables and about the types of Variables --&gt;</mark>

<mark>&lt;-- Now, in the next part we will discuss about the use of conditional logics with the if-else cases in the Terraform. --&gt;</mark>