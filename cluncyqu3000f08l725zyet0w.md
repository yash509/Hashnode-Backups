---
title: "Deep Dive into Terraform - P7 (Deployment of AWS NACL, Inbound & Outbound Routes, Security Group & associating it with the Subnet Using Terraform)"
datePublished: Sat Apr 06 2024 00:30:14 GMT+0000 (Coordinated Universal Time)
cuid: cluncyqu3000f08l725zyet0w
slug: deep-dive-into-terraform-p7-deployment-of-aws-nacl-inbound-outbound-routes-security-group-associating-it-with-the-subnet-using-terraform
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1711955134844/c4e85a03-4118-4482-9b41-be3c31e2b2eb.png
tags: cloud, aws, azure, devops, terraform, infrastructure-as-code, gcp, devsecops, 2articles1week, technical-writing-1, devops-articles, terraform-cloud, infrastructure-management, terraform-aws-infrastructureascode-provisioning-automation-cloudcomputing, terraform-terraform-cloud-devops-devops-articles-devsecops-cloud-aws-gcp-azure-terraform-aws-infrastructureascode-provisioning-automation-cloudcomputing-infrastructure-as-code-terraform-state-technical-writing-blogging-infrastructure-management

---

In the previous parts of the Terraform series we had discussed about each and every important topic of Terraform along with an example of Deploying of AWS EC2 instance with the Security Group & the User Data using Terraform.

So, in this part of the terraform series we will be discussing about one more example of the terraform in which we will be going to Deploy the AWS NACL, Inbound & Outbound Routes, Security Group & associating it with the Subnet Using Terraform.

This time also we are deploying the following resources on AWS. So, that means will be using the AWS provider again.

Let's Go....

```plaintext
provider "aws" {
  region = "ap-south-1" # AWS region
}

# Creation of a network access control list
resource "aws_network_acl" "example" {
  vpc_id = aws_vpc.example.id
}

# Creation of the inbound and the outbound rules for the network access control list
resource "aws_network_acl_rule" "example_inbound" {
  network_acl_id = aws_network_acl.example.id
  rule_number    = 100
  protocol       = "tcp"
  rule_action    = "allow"
  cidr_block     = "0.0.0.0/0"
  egress         = false
  from_port      = 80
  to_port        = 80

  network_acl_id = aws_network_acl.example.id
  rule_number    = 200
  protocol       = "tcp"
  rule_action    = "allow"
  cidr_block     = "0.0.0.0/0"
  egress         = false
  from_port      = 22
  to_port        = 22
 
  network_acl_id = aws_network_acl.example.id
  rule_number    = 300
  protocol       = "tcp"
  rule_action    = "allow"
  cidr_block     = "0.0.0.0/0"
  egress         = false
  from_port      = 3001
  to_port        = 64317
}

resource "aws_network_acl_rule" "example_outbound" {
  network_acl_id = aws_network_acl.example.id
  rule_number    = 400
  protocol       = "tcp"
  rule_action    = "allow"
  cidr_block     = "0.0.0.0/0"
  egress         = true
  from_port      = 0
  to_port        = 65535
}

# Creation of a security group
resource "aws_security_group" "example_name" {
  name        = "example"
  description = "Example Security Group"
  vpc_id = aws_vpc.example.id

  ingress {
    from_port   = 0
    to_port     = 65535
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  ingress {
    from_port   = 443
    to_port     = 443
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  ingress {
    from_port   = 80
    to_port     = 80
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }
  
  ingress {
    from_port   = 23
    to_port     = 22
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  egress {
    from_port   = 0
    to_port     = 65535
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }
}

# Associate security group with subnet
resource "aws_security_group_association" "example" {
  subnet_id      = aws_subnet.example.id
  security_group = aws_security_group.example.id
}

# Define your VPC and subnet
resource "aws_vpc" "example" {
  cidr_block = "10.0.0.0/16"
}

resource "aws_subnet" "example" {
  vpc_id                  = aws_vpc.example.id
  cidr_block              = "10.0.1.0/24"
  availability_zone       = "ap-south-1a" # AZ of your choice
}
```

Make sure to replace the following values like `ap-soth-1`, `10.0.0.0/16`, `10.0.1.0/24`, etc., with your desired values according to your AWS environment and requirements. Moreover, adjust the inbound and outbound rules, security group settings, and other parameters as needed for your specific use cases.

1. Run `terraform fmt` command to rewrite the Terraform configuration files to a canonical format:
    
    ```plaintext
     terraform fmt
    ```
    
2. Run `terraform init` command to initialize the Terraform directory and download all the necessary plugins:
    
    ```plaintext
     terraform init
    ```
    
    **Console Output of**`terraform init`**command:-**
    
    ```powershell
    Initializing the backend...
    
    Initializing provider plugins...
    - Checking for available provider plugins...
    - Downloading plugin for provider "aws" (hashicorp/aws) 3.62.0...
    
    Terraform has been successfully initialized!
    ```
    
3. Run `terraform plan` command to see what Terraform is planning to do upon running the apply command:
    
    ```plaintext
     terraform plan
    ```
    
    **Console output of**`terraform plan`**command:-**
    
    ```rust
    Refreshing Terraform state in-memory prior to plan...
    The refreshed state will be used to calculate this plan, but will not be persisted to local or remote state storage.
    
    Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
      + create
    
    Terraform will perform the following actions:
    
      # aws_network_acl.example will be created
      + resource "aws_network_acl" "example" {
          + arn           = (known after apply)
          + default_egress = (known after apply)
          + default_egress_action = (known after apply)
          + default_egress_cidr_block = (known after apply)
          + default_egress_ipv6_cidr_block = (known after apply)
          + default_egress_port_range {
              + from_port = (known after apply)
              + to_port   = (known after apply)
            }
          + default_egress_protocol = "-1"
          + default_egress_rule_id   = (known after apply)
          + default_ingress          = (known after apply)
          + default_ingress_action   = (known after apply)
          + default_ingress_cidr_block = (known after apply)
          + default_ingress_ipv6_cidr_block = (known after apply)
          + default_ingress_port_range {
              + from_port = (known after apply)
              + to_port   = (known after apply)
            }
          + default_ingress_protocol = "-1"
          + default_ingress_rule_id = (known after apply)
          + id                       = (known after apply)
          + owner_id                 = (known after apply)
          + subnet_ids               = (known after apply)
          + tags                     = {
              + "Name" = "example"
            }
          + vpc_id                   = (known after apply)
        }
    ```
    
    ```rust
     # aws_network_acl_rule.example_inbound will be created
      + resource "aws_network_acl_rule" "example_inbound" {
          + cidr_block              = "0.0.0.0/0"
          + egress                  = false
          + from_port               = 3001
          + id                      = (known after apply)
          + icmp_type               = ""
          + ipv6_cidr_block         = ""
          + network_acl_id          = (known after apply)
          + protocol                = "6"
          + rule_action             = "allow"
          + rule_number             = 300
          + to_port                 = 64317
        }
    
      # aws_network_acl_rule.example_outbound will be created
      + resource "aws_network_acl_rule" "example_outbound" {
          + cidr_block              = "0.0.0.0/0"
          + egress                  = true
          + from_port               = 0
          + id                      = (known after apply)
          + icmp_type               = ""
          + ipv6_cidr_block         = ""
          + network_acl_id          = (known after apply)
          + protocol                = "6"
          + rule_action             = "allow"
          + rule_number             = 400
          + to_port                 = 65535
        }
    ```
    
    ```rust
     # aws_security_group.example_name will be created
      + resource "aws_security_group" "example_name" {
          + arn                    = (known after apply)
          + description            = "Example Security Group"
          + egress                 = (known after apply)
          + id                     = (known after apply)
          + ingress                = (known after apply)
          + name                   = "example"
          + owner_id               = (known after apply)
          + revoke_rules_on_delete = false
          + tags                   = (known after apply)
          + vpc_id                 = (known after apply)
        }
    
      # aws_security_group_association.example will be created
      + resource "aws_security_group_association" "example" {
          + id                   = (known after apply)
          + security_group_id    = (known after apply)
          + subnet_id            = (known after apply)
          + vpc_id               = (known after apply)
        }
    
      # aws_subnet.example will be created
      + resource "aws_subnet" "example" {
          + arn                             = (known after apply)
          + assign_ipv6_address_on_creation = false
          + availability_zone               = "ap-south-1a"
          + availability_zone_id            = (known after apply)
          + cidr_block                      = "10.0.1.0/24"
          + id                              = (known after apply)
          + ipv6_cidr_block                 = (known after apply)
          + ipv6_cidr_block_association_id  = (known after apply)
          + map_public_ip_on_launch         = false
          + owner_id                        = (known after apply)
          + vpc_id                          = (known after apply)
        }
    
      # aws_vpc.example will be created
      + resource "aws_vpc" "example" {
          + arn                              = (known after apply)
          + assign_generated_ipv6_cidr_block = false
          + cidr_block                       = "10.0.0.0/16"
          + default_network_acl_id           = (known after apply)
          + default_route_table_id           = (known after apply)
          + default_security_group_id        = (known after apply)
          + dhcp_options_id                  = (known after apply)
          + enable_classiclink               = (known after apply)
          + enable_classiclink_dns_support   = (known after apply)
          + id                               = (known after apply)
          + instance_tenancy                 = (known after apply)
          + ipv6_association_id              = (known after apply)
          + ipv6_cidr_block                  = (known after apply)
          + main_route_table_id              = (known after apply)
          + owner_id                         = (known after apply)
          + tags                             = (known after apply)
        }
    
    Plan: 7 to add, 0 to change, 0 to destroy.
    ```
    
4. Run `terraform apply` command to apply the changes and create the resources:
    
    ```plaintext
     terraform apply --auto-approve
    ```
    
    **Console output of**`terraform apply --auto-approve`**command:-**
    
    ```rust
    aws_vpc.example: Creating...
    aws_vpc.example: Creation complete after 5s [id=vpc-0123456789abcdef0]
    
    aws_subnet.example: Creating...
    aws_subnet.example: Creation complete after 3s [id=subnet-0123456789abcdef1]
    
    aws_network_acl.example: Creating...
    aws_network_acl.example: Creation complete after 1s [id=acl-0123456789abcdef2]
    
    aws_security_group.example_name: Creating...
    aws_security_group.example_name: Creation complete after 2s [id=sg-0123456789abcdef3]
    
    aws_network_acl_rule.example_inbound: Creating...
    aws_network_acl_rule.example_inbound: Creation complete after 1s [id=acl-0123456789abcdef2-100]
    aws_network_acl_rule.example_inbound: Creating...
    aws_network_acl_rule.example_inbound: Creation complete after 1s [id=acl-0123456789abcdef2-200]
    aws_network_acl_rule.example_inbound: Creating...
    aws_network_acl_rule.example_inbound: Creation complete after 1s [id=acl-0123456789abcdef2-300]
    
    aws_network_acl_rule.example_outbound: Creating...
    aws_network_acl_rule.example_outbound: Creation complete after 1s [id=acl-0123456789abcdef2-400]
    
    aws_security_group_association.example: Creating...
    aws_security_group_association.example: Creation complete after 1s [id=sga-0123456789abcdef4]
    
    Apply complete! Resources: 7 added, 0 changed, 0 destroyed.
    ```
    
5. And once we are done with our work we will now destroy all the resources that we had created:
    
    ```plaintext
     terraform destroy --auto-approve
    ```
    
    This command will remove all the resources created by Terraform.
    

*<mark>&lt;-- In this part we created </mark>* <mark>the AWS NACL, Inbound &amp; Outbound Routes, Security Group &amp; associating it with the Subnet Using Terraform</mark>*<mark>--&gt;</mark>*

*<mark>&lt;-- In the next part of Terraform Series we will see the another example of Terraform. --&gt;</mark>*