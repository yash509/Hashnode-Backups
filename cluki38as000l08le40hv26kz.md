---
title: "Deep Dive into Terraform - P5 
(Terraform Conditional Logics)"
datePublished: Thu Apr 04 2024 00:30:23 GMT+0000 (Coordinated Universal Time)
cuid: cluki38as000l08le40hv26kz
slug: deep-dive-into-terraform-p5-terraform-conditional-logics
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1711882805609/ac366642-c9f6-428a-a0d1-a3d0cf399bb2.png
tags: cloud, blogging, aws, azure, devops, terraform, infrastructure-as-code, gcp, devsecops, 2articles1week, devops-articles, terraform-cloud, infrastructure-management, terraform-aws-infrastructureascode-provisioning-automation-cloudcomputing, terraform-conditional-expression

---

Before moving ahead and start discussing about the Conditional logics with If/else cases in Terraform and their examples. Let's take the quick overview on the various previous aspects of Infrastructure as Code, Terraform, Terraform State, and Terraform Variables.

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

# **What are Terraform Variables?**

The Terraform Variables are one of the fundamental elements in the Infrastructure as Code (IaC) workflows, providing flexibility, reusability, and dynamic nature to the infrastructure configurations. The terraform variables are the kind of tools for managing infrastructure configurations in a dynamically and scalable manner, by understanding their types, patterns, and other best practices, the developers or the DevOps Engineers can use the full potential of variables to enhance their infrastructure as code (IaC) workflows, it improves the code maintainability, and can achieve great help in the management of infrastructure. Basically, the variables in Terraform serve as placeholders for the dynamic values, by allowing for reusability and adaptability of the configurations, from defining resource attributes, configuring environments, or managing sensitive information, in every aspect the terraform variables plays a crucial role.

---

# What are the Conditional Logics or Statements in Terraform?

In Terraform, the conditional statements are important for managing the infrastructure configurations based on given conditions, and these given conditions can vary from environment variables to resource availability or to any other dynamic factors. The terraform provides several mechanisms for implementing conditional logic or the statements within the terraform configuration files. Basically, in other words we can say that in terraform the conditional statements are used to control the behavior of your infrastructure deployments based on given certain conditions. Imagine you're writing a paragraph where you only want to include certain sentences if a particular condition is met. In Terraform, we can use the conditional statements in various ways to control the behavior of our infrastructure deployment.

What is the conditional structure of Terraform?

```plaintext
condition ? true_val : false_val
```

However, the Terraform doesn't provide any traditional programming constructs or concepts like if-else statements, it only offers some sort of mechanisms to achieve the similar functionalities like:

1. Count Parameter:- You can use `count` parameter to create multiple cases of a resource based on a given condition. For example:
    
    ```plaintext
    resource "aws_instance" "example" {
      count = var.create_instance ? 1 : 0
    }
    ```
    
    Above we can see that, the `var.create_instance` is a boolean variable that determines whether to create the `aws_instance` or not.
    
2. Conditional Expression: We can use conditional expressions to set resource's characteristics on basis of conditions. For example:
    
    ```plaintext
    resource "aws_instance" "example" {
      ami           = var.create_instance ? "ami-65874379e241" : "ami-87464328yiu98"
      instance_type = var.create_instance ? "t3.medium" : "t3.large"
    }
    ```
    
3. Dynamic Blocks:- We can use dynamic blocks to conditionally include blocks of configurations. For example:
    
    ```plaintext
    resource "aws_instance" "example" {
      // Configuration for your instance...
    
      # Only attach storage if attach_storage variable is true
      dynamic "ebs_block_device" {
        for_each = var.attach_storage == true ? [1] : []
        content {
          // Configuration for your storage...
        }
      }
    }
    ```
    
    In this above example, We're using a `dynamic` block, which allows us to create resources conditionally. The `for_each` expression evaluates whether the `attach_storage` variable is true. If `attach_storage` is true, Terraform will create an EBS block device for storage. Otherwise, it will not include this block in the deployment plan. So, from this example of Dynamic Blocks we can conclude that "If we need to attach storage because `attach_storage` is true, include this configuration for the storage. Otherwise, skip it." This helps in making your infrastructure deployments more flexible and adaptable to different scenarios.
    

*<mark>&lt;-- In this part of Terraform Series we discussed about the Terraform Conditional Logics or Statements. --&gt;</mark>*

*<mark>&lt;-- Now, in the next part we will see the various examples of Infrastructure provisioning on AWS by using the Terraform --&gt;</mark>*