---
title: "Deep Dive into Terraform - P9 (Deployment of AWS EKS Cluster, Cluster's Node Group, IAM Roles and Remote Backend to store State file using Terraform)"
datePublished: Mon Apr 08 2024 00:30:17 GMT+0000 (Coordinated Universal Time)
cuid: cluq7ui9g000308jo16ttech8
slug: deep-dive-into-terraform-p9-deployment-of-aws-eks-cluster-clusters-node-group-iam-roles-and-remote-backend-to-store-state-file-using-terraform
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1711976918594/bd1e611b-ab88-430c-8d6c-888a6214d366.png
tags: cloud, blogging, aws, azure, devops, terraform, infrastructure-as-code, gcp, devsecops, 2articles1week, technical-writing-1, devops-articles, terraform-cloud, infrastructure-management, terraform-aws-infrastructureascode-provisioning-automation-cloudcomputing

---

In the previous parts of the Terraform series we had discussed about each and every important topic of Terraform along with the examples like Deploying of AWS EC2 instance with the Security Group & the User Data using Terraform, Deployment of AWS NACL, Inbound & Outbound Routes, Security Group & associating it with the Subnet using Terraform, and Deployment of AWS Private Subnet, NAT Gateway, Elastic IP, Private Route Table using Terraform.

So, in this part of the terraform series we will be discussing about one more example of the terraform in which we will be going to Deploy AWS EKS Cluster, Cluster's Node Group, some IAM Roles and Remote Backend to store State file using Terraform.

This time also we are deploying the following resources on AWS. So, that means will be using the AWS provider again.

Moreover, in this mini project of the Deployment of AWS EKS Cluster, Cluster's Node Group, IAM Roles and Remote Backend to store State file using Terraform, we will be using the discrete files structure to define the terraform configurations. For example:- we will be creating the separate files for defining the AWS provider, S3 Backend and for EKS Cluster, IAM roles, Node Group.

Let's Go....

`provider.tf` file for defining the AWS provider:-

```powershell
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 5.0"
    }
  }
}

# Configure the AWS Provider
provider "aws" {
  region = "ap-south-1"
}
```

`main.tf` file which contains the code for initializing the EKS Cluster, Node Group, and the IAM roles for the both Cluster and Node Group:-

```powershell
data "aws_iam_policy_document" "assume_role" {
  statement {
    effect = "Allow"

    principals {
      type        = "Service"
      identifiers = ["eks.amazonaws.com"]
    }

    actions = ["sts:AssumeRole"]
  }
}

resource "aws_iam_role" "example" {
  name               = "eks-cluster-cloud"
  assume_role_policy = data.aws_iam_policy_document.assume_role.json
}

resource "aws_iam_role_policy_attachment" "example-AmazonEKSClusterPolicy" {
  policy_arn = "arn:aws:iam::aws:policy/AmazonEKSClusterPolicy"
  role       = aws_iam_role.example.name
}

# VPC
data "aws_vpc" "default" {
  default = true
}
# public subnets for EKS cluster
data "aws_subnets" "public" {
  filter {
    name   = "vpc-id"
    values = [data.aws_vpc.default.id]
  }
}

# EKS Cluster
resource "aws_eks_cluster" "example" {
  name     = "App-Cluster" # This name can be changed
  role_arn = aws_iam_role.example.arn

  vpc_config {
    subnet_ids = data.aws_subnets.public.ids
  }

  # Ensure that IAM Role permissions are created before and deleted after EKS Cluster handling.
  # Otherwise, EKS will not be able to properly delete EKS managed EC2 infrastructure such as Security Groups.
  depends_on = [
    aws_iam_role_policy_attachment.example-AmazonEKSClusterPolicy,
  ]
}

resource "aws_iam_role" "example1" {
  name = "eks-node-group-cloud"

  assume_role_policy = jsonencode({
    Statement = [{
      Action = "sts:AssumeRole"
      Effect = "Allow"
      Principal = {
        Service = "ec2.amazonaws.com"
      }
    }]
    Version = "2012-10-17"
  })
}

resource "aws_iam_role_policy_attachment" "example-AmazonEKSWorkerNodePolicy" {
  policy_arn = "arn:aws:iam::aws:policy/AmazonEKSWorkerNodePolicy"
  role       = aws_iam_role.example1.name
}

resource "aws_iam_role_policy_attachment" "example-AmazonEKS_CNI_Policy" {
  policy_arn = "arn:aws:iam::aws:policy/AmazonEKS_CNI_Policy"
  role       = aws_iam_role.example1.name
}

resource "aws_iam_role_policy_attachment" "example-AmazonEC2ContainerRegistryReadOnly" {
  policy_arn = "arn:aws:iam::aws:policy/AmazonEC2ContainerRegistryReadOnly"
  role       = aws_iam_role.example1.name
}

# Cluster's Node Group
resource "aws_eks_node_group" "example" {
  cluster_name    = aws_eks_cluster.example.name
  node_group_name = "Node-Port-App" # This name can be changed
  node_role_arn   = aws_iam_role.example1.arn
  subnet_ids      = data.aws_subnets.public.ids

  scaling_config {
    desired_size = 1
    max_size     = 2
    min_size     = 1
  }
  instance_types = ["t2.medium"]

  # Ensure that IAM Role permissions are created before and deleted after EKS Node Group handling.
  # Otherwise, EKS will not be able to properly delete EC2 Instances and Elastic Network Interfaces.
  depends_on = [
    aws_iam_role_policy_attachment.example-AmazonEKSWorkerNodePolicy,
    aws_iam_role_policy_attachment.example-AmazonEKS_CNI_Policy,
    aws_iam_role_policy_attachment.example-AmazonEC2ContainerRegistryReadOnly,
  ]
}
```

`backend.tf` file for creating the AWS S3 bucket which will serves as the Remote Backend for storing the `terraform.tfstate` file in the remote backend in S3 Bucket:

```powershell
terraform {
  backend "s3" {
    bucket = "backend-js-app" # Replace with your actual S3 bucket name
    key    = "terraform.tfstate"
    region = "ap-south-1"
  }
}
```

Now, we are ready to run the below commands to deploy the mentioned infrastructure on AWS platform.

1. Run `terraform fmt` command to rewrite the Terraform configuration files to a canonical format:
    
    ```powershell
       terraform fmt
    ```
    
2. Run `terraform init` command to initialize the Terraform directory and download all the necessary plugins:
    
    ```powershell
       terraform init
    ```
    
3. Run `terraform plan` command to see what Terraform is planning to do upon running the apply command:
    
    ```powershell
       terraform plan
    ```
    
4. Run `terraform apply` command to apply the changes:
    
    ```powershell
    terraform apply --auto-approve
    ```
    
5. And once we are done with our work we will now destroy all the resources that we had created:
    
    ```powershell
       terraform destroy --auto-approve
    ```
    

*<mark>&lt;-- In this part we created </mark>* <mark>the AWS AWS EKS Cluster, Cluster's Node Group, IAM Roles and Remote Backend to store State file using Terraform</mark>*<mark>--&gt;</mark>*

*<mark>&lt;-- In the next part of Terraform Series we will see the another example of Terraform. --&gt;</mark>*