---
title: "Deep Dive into Terraform - P8 (Deployment of AWS Private Subnet, NAT Gateway, Elastic IP, Private Route Table using Terraform)"
datePublished: Sun Apr 07 2024 00:30:41 GMT+0000 (Coordinated Universal Time)
cuid: cluosf6cx000g08jv7eskcstq
slug: deep-dive-into-terraform-p8-deployment-of-aws-private-subnet-nat-gateway-elastic-ip-private-route-table-using-terraform
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1711972642958/a5cf4344-85e9-4235-9528-1d379d1da881.png
tags: cloud, blogging, aws, azure, devops, terraform, infrastructure-as-code, gcp, devsecops, 2articles1week, technical-writing-1, devops-articles, terraform-cloud, infrastructure-management, terraform-aws-infrastructureascode-provisioning-automation-cloudcomputing

---

In the previous parts of the Terraform series we had discussed about each and every important topic of Terraform along with the examples like Deploying of AWS EC2 instance with the Security Group & the User Data using Terraform and Deployment of AWS NACL, Inbound & Outbound Routes, Security Group & associating it with the Subnet Using Terraform.

So, in this part of the terraform series we will be discussing about one more example of the terraform in which we will be going to Deploy AWS Private Subnet, NAT Gateway, Elastic IP, Private Route Table using Terraform.

This time also we are deploying the following resources on AWS. So, that means will be using the AWS provider again.

Let's Go....

```rust
provider "aws" {
  region = "ap-south-1" // AWS region
}

// VPC configuration
resource "aws_vpc" "example" {
  cidr_block = "10.0.0.0/16"
}

// Internet Gateway
resource "aws_internet_gateway" "example" {
  vpc_id = aws_vpc.example.id
}

// Subnet configuration
resource "aws_subnet" "private_subnet" {
  vpc_id                  = aws_vpc.example.id
  cidr_block              = "10.0.1.0/24"
  availability_zone       = "ap-south-1a" // AZ can be changed as per choice 
  map_public_ip_on_launch = false
}

// Elastic IP
resource "aws_eip" "example" {}

// NAT Gateway
resource "aws_nat_gateway" "example" {
  allocation_id = aws_eip.example.id
  subnet_id     = aws_subnet.private_subnet.id
}

// Private Route Table
resource "aws_route_table" "private_route_table" {
  vpc_id = aws_vpc.example.id
}

// Route for NAT Gateway
resource "aws_route" "private_route" {
  route_table_id         = aws_route_table.private_route_table.id
  destination_cidr_block = "0.0.0.0/0"
  nat_gateway_id         = aws_nat_gateway.example.id
}

// Associating the Subnet with Route Table
resource "aws_route_table_association" "private_subnet_association" {
  subnet_id      = aws_subnet.private_subnet.id
  route_table_id = aws_route_table.private_route_table.id
}
```

1. Run `terraform fmt` command to rewrite the Terraform configuration files to a canonical format:
    
    ```powershell
      terraform fmt
    ```
    
2. Run `terraform init` command to initialize the Terraform directory and download all the necessary plugins:
    
    ```powershell
      terraform init
    ```
    
    **Console Output of** `terraform init` **command:-**
    
    ```powershell
    Initializing the backend...
    
    Initializing provider plugins...
    - Checking for available provider plugins...
    - Downloading plugin for provider "aws" (hashicorp/aws) 3.62.0...
    
    Terraform has been successfully initialized!
    ```
    
3. Run `terraform plan` command to see what Terraform is planning to do upon running the apply command:
    
    ```rust
      terraform plan
    ```
    
    **Console output of**`terraform plan`**command:-**
    
    ```rust
    Terraform will perform the following actions:
    
      # aws_eip.example will be created
      + resource "aws_eip" "example" {
          + allocation_id   = (known after apply)
          + association_id  = (known after apply)
          + domain          = (known after apply)
          + id              = (known after apply)
          + instance        = (known after apply)
          + network_interface = (known after apply)
          + private_dns     = (known after apply)
          + private_ip      = (known after apply)
          + public_dns      = (known after apply)
          + public_ip       = (known after apply)
          + public_ipv4_pool = (known after apply)
          + vpc             = true
        }
    
      # aws_internet_gateway.example will be created
      + resource "aws_internet_gateway" "example" {
          + arn      = (known after apply)
          + id       = (known after apply)
          + owner_id = (known after apply)
          + vpc_id   = (known after apply)
        }
    
      # aws_nat_gateway.example will be created
      + resource "aws_nat_gateway" "example" {
          + allocation_id        = (known after apply)
          + id                   = (known after apply)
          + network_interface_id = (known after apply)
          + private_ip           = (known after apply)
          + public_ip            = (known after apply)
          + subnet_id            = (known after apply)
          + tags                 = {
              + "Name" = "terraform-example"
            }
        }
    
      # aws_route.private_route will be created
      + resource "aws_route" "private_route" {
          + destination_cidr_block = "0.0.0.0/0"
          + gateway_id             = (known after apply)
          + id                     = (known after apply)
          + instance_id            = (known after apply)
          + ipv6_cidr_block        = (known after apply)
          + local_gateway_id       = (known after apply)
          + nat_gateway_id         = (known after apply)
          + network_interface_id   = (known after apply)
          + route_table_id         = (known after apply)
          + transit_gateway_id     = (known after apply)
          + vpc_peering_connection_id = (known after apply)
        }
    
      # aws_route_table.private_route_table will be created
      + resource "aws_route_table" "private_route_table" {
          + arn              = (known after apply)
          + id               = (known after apply)
          + owner_id         = (known after apply)
          + propagating_vgws = (known after apply)
          + route            = (known after apply)
          + route_table_id   = (known after apply)
          + tags             = {
              + "Name" = "private"
            }
          + vpc_id           = (known after apply)
        }
    
      # aws_route_table_association.private_subnet_association will be created
      + resource "aws_route_table_association" "private_subnet_association" {
          + id             = (known after apply)
          + route_table_id = (known after apply)
          + subnet_id      = (known after apply)
        }
    
      # aws_subnet.private_subnet will be created
      + resource "aws_subnet" "private_subnet" {
          + arn                             = (known after apply)
          + assign_ipv6_address_on_creation = false
          + availability_zone               = "ap-south-1a"
          + cidr_block                      = "10.0.1.0/24"
          + id                              = (known after apply)
          + ipv6_cidr_block                 = (known after apply)
          + ipv6_cidr_block_association_id  = (known after apply)
          + map_customer_owned_ip_on_launch = false
          + map_public_ip_on_launch         = false
          + outpost_arn                     = (known after apply)
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
          + enable_dns_hostnames             = (known after apply)
          + enable_dns_support               = true
          + id                               = (known after apply)
          + instance_tenancy                 = (known after apply)
          + ipv6_association_id              = (known after apply)
          + ipv6_cidr_block                  = (known after apply)
          + main_route_table_id              = (known after apply)
          + owner_id                         = (known after apply)
          + tags                             = {
              + "Name" = "terraform-example"
            }
        }
    
    Plan: 9 to add, 0 to change, 0 to destroy.
    ```
    
4. Run `terraform apply` command to apply the changes and create the EC2 instance, security group, etc:
    
    ```rust
      terraform apply --auto-approve
    ```
    
    **Console output of**`terraform apply --auto-approve`**command:-**
    
    ```rust
    aws_vpc.example: Creating...
    aws_vpc.example: Creation complete after 2s [id=vpc-0c144c579b6907b8e]
    aws_subnet.private_subnet: Creating...
    aws_subnet.private_subnet: Creation complete after 1s [id=subnet-0219d712f44f4b89e]
    aws_internet_gateway.example: Creating...
    aws_internet_gateway.example: Creation complete after 1s [id=igw-0f67a1244b1a27241]
    aws_eip.example: Creating...
    aws_eip.example: Creation complete after 1s [id=eipalloc-076a5e9d2d58d6f4a]
    aws_nat_gateway.example: Creating...
    aws_nat_gateway.example: Creation complete after 1m [id=nat-0e6547b5bfa2df5d1]
    aws_route_table.private_route_table: Creating...
    aws_route_table.private_route_table: Creation complete after 1s [id=rtb-036ef9a527f52d271]
    aws_route.private_route: Creating...
    aws_route.private_route: Creation complete after 1s [id=r-rtb-036ef9a527f52d2710.0.0.0/0]
    
    Apply complete! Resources: 9 added, 0 changed, 0 destroyed.
    ```
    
5. And once we are done with our work we will now destroy all the resources that we had created:
    
    ```rust
      terraform destroy --auto-approve
    ```
    
    This command will remove all the resources created by Terraform.
    

*<mark>&lt;-- In this part we created </mark>* <mark>the AWS Private Subnet, NAT Gateway, Elastic IP, Private Route Table using Terraform</mark>*<mark>--&gt;</mark>*

*<mark>&lt;-- In the next part of Terraform Series we will see the another example of Terraform. --&gt;</mark>*