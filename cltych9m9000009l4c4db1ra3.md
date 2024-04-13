---
title: "A step ahead of Terraform: Introduction to the Terragrunt"
datePublished: Tue Mar 19 2024 12:22:24 GMT+0000 (Coordinated Universal Time)
cuid: cltych9m9000009l4c4db1ra3
slug: a-step-ahead-of-terraform-introduction-to-the-terragrunt
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1710846245968/4fe62902-2bf4-41aa-92c5-cfae9213256a.png
tags: cloud, aws, azure, devops, terraform, infrastructure-as-code, gcp, terragrunt

---

### **What Is Terragrunt?**

Terragrunt is a open source tool for managing Terraform configurations developed by GruntWork that helps to reduce code duplication across your Terraform projects because it effectively keeps your terraform code DRY. Terraform is a popular Infrastructure as Code (IaC) tool used for defining and provisioning infrastructure resources on various cloud platforms such as AWS, GCP, and Azure such as virtual machines, networks, storage, etc. While Terraform allows users to define infrastructure configurations in code, Terragrunt adds additional features and enhancements to make managing Terraform configurations easily and with more scalability. Overall, Terragrunt enhances the usability and scalability of Terraform configurations, making it easier for teams to manage infrastructure as code in complex environments.

DRY (**Do not Repeat Yourself**) is a sort of configuration that allows users to avoid duplication of code by providing mechanisms for reusing of the code across various multiple Terraform configurations.

Some key features of Terragrunt are as follows:

1. State Management (Remotely):- Terragrunt simplifies the management of Terraform remote state by automatically configuring remote state storage and locking, which helps prevent conflicts when multiple users are working on the same infrastructure.
    
2. Dependency and Environment management:- Terragrunt enables users to define dependencies between Terraform modules, ensuring that modules are applied in the correct order and Terragrunt facilitates managing multiple environments by allowing users to define configuration overrides and variable values for each environment.
    

The term, Terragrunt can be used to manage Terraform codes across the multiple environments, multiple AWS, GCP and Azure accounts, etc. The terragrunt streamlines the orchestration of multiple environments by establishing a distinct segregation between them. Terragrunt introduces hooks, which are a sort of powerful triggers for executing actions before or after Terraform commands are run. These hooks provide a flexible mechanism for the integration of various behaviors into the Terraform workflow.

Most Importantly, the Terragrunt can also be integrated with your CI/CD pipelines for automatic infrastructure deployment on various cloud platforms such as AWS, GCP and Azure.

The terragrunt can also be integrated with external secret management tools, such as HashiCorp Vault or AWS Secrets Manager, enabling secure handling of sensitive data within Terraform configurations. The terragrunt's integration with external secret management tools powers up the users to maintain a robust security measures while streamlining the management of sensitive data within theTerraform workflows.

Some Terragrunt commands which can be used in place of basic Terraform commands are as follows:-

1. `terragrunt init`
    
2. `terragrunt plan`
    
3. `terragrunt apply`
    
4. `terragrunt output`
    
5. `terragrunt destroy`
    

## Revolution that the Terragrunt brought in the AWS

Terragrunt revolutionizes the AWS credential management by offering a secure and flexible approach to specifying IAM roles for deployment. With the `--terragrunt-iam-role` CLI argument or the `TERRAGRUNT_IAM_ROLE` environmental variable, users can effortlessly define the IAM role to be utilized during infrastructure provisioning. The terragrunt intelligently employs the `sts-assume-role` API, enabling the seamless retrieval of temporary credentials. Which makes it possible to seamlessly deployment of infrastructure across different environments without having to store AWS credentials in plaintext. The terragrunt's support for specifying IAM roles represents a paradigm shift in AWS credential management, offering a potent solution for securely deploying infrastructure across various environments without compromising on security or convenience.

## **Installation of Terragrunt**

To install the Terragrunt, make sure you have already installed the Terraform before.

* Follow this [link](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli) to install Terraform.
    
* Download the Terragrunt binary from the [here](https://github.com/gruntwork-io/terragrunt/releases).
    
* Select the correct binary for your Operating System.
    
* Copy the link and download on your terminal using the wget command. For Example: `wget https://github.com/gruntwork-io/terragrunt/releases/download/v0.54.19/terragrunt_linux_amd64`
    
* Rename the binary to terragrunt: `mv terragrunt_linux_amd64 terragrunt`
    
* Make the file executable by using the command: `chmod u+x terragrunt`
    
* Move the file to the `/usr/local/bin` directory using the command: \`sudo mv terragrunt /usr/local/bin/terragrunt'
    
* To verify your installation, run the command: `terragrunt --version`.
    

## **Case Study**

Let's see a scenario for managing infrastructure with Terragrunt.

The following is a sample of a terraform code for creating an EC2 instance using Terraform:-

```plaintext
terraform {
required_providers {
    aws = {
        source = "hashicorp/aws"
        version = "~> 4.16"
        }
    }
    required_version = ">= 1.2.0"
}

provider "aws" {
    region = "us-west-2"
}

resource "aws_instance" "app_server" {
ami = "ami-830c94e3"
instance_type = "t2.micro"

tags = {
    Name = "ExampleAppServerInstance"
    }
}
```

**In this we can see the main problem is that, how do you create this instance across several environments?**

Ordinarily, you wants to duplicate the same code for each environment and then modify the parameters. You may wish to specify different instance types for each environment. For example, you might want to use a t2.micro instance for development environment, a t3.medium for test environment and a t2.large for production.

The problem is that this would be a very manual process -inefficient and leaves plenty room for errors. Using Terragrunt, we can improve this code without having to copy and paste the code across several environments.

Also these environments might be spread out across different AWS accounts and you'd also have to worry about managing the different AWS credentials and IAM roles required. The terraform backend does not support variables or any type of expression whatsoever. So you would have to manually copy and edit the backend configuration code for each of the environments.

## **Working With Terragrunt**

First we need to create seperate directories for each of the enviornments like `test` `production` and `dev` In each of the directories, a `terragrunt.hcl` file will be created.

This is how `terragrunt.hcl` file looks like:

```plaintext
terraform {
    source = "tfr:///terraform-aws-modules/ec2-instance/aws?version=5.6.0"
}

generate "provider" {
    path = "provider.tf"
    if_exists = "overwrite_terragrunt"
    contents = <<EOF
    provider "aws" {
        profile = "default"
        region = "us-east-1"
        }
    EOF
}

inputs = {
    ami = "ami-0005e0cfe09cc9050"
    instance_type = "t2.micro"
    tags = {
        Name = "grunt-ec2"
        }
    }
```

Now In the case I have to replicate this in my `test` directory with a very few changes. The instance type for `test` directory will be t2.medium, the tags have also been modified to reflect the environment.

This is how `terragrunt.hcl` of `test` environment looks like:

```plaintext
terraform {
    source = "tfr:///terraform-aws-modules/ec2-instance/aws?version=5.6.0"
}

generate "provider" {
    path = "provider.tf"
    if_exists = "overwrite_terragrunt"
    contents = <<EOF
    provider "aws" {
        profile = "default"
        region = "us-east-1"
        }
    EOF
}

inputs = {
    ami = "ami-0005e0cfe09cc9050"
    instance_type = "t2.medium"
    tags = {
        Name = "grunt-test-ec2"
        Environment = "test"
        }
    }
```

The next stage is to execute terragrunt commands to read our configuration and invoke terraform with it.

* Switch to the `dev` directory.
    
* First, run the command `terragrunt init`.
    
* Now run `terragrunt plan` command to see proposed infrastructure changes.
    
* Then, Finally run `terragrunt apply` command to actually create the instance.