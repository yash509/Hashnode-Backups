---
title: "Deep Dive into Terraform - P6 (Deployment of AWS EC2 instance with the Security Group & the User Data Using Terraform)"
datePublished: Fri Apr 05 2024 00:30:38 GMT+0000 (Coordinated Universal Time)
cuid: clulxjexs000208l7brog57uq
slug: deep-dive-into-terraform-p6-deployment-of-aws-ec2-instance-with-the-security-group-the-user-data-using-terraform
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1711951878934/3be8e7c5-105f-47aa-9358-11757c3aa464.png
tags: cloud, aws, azure, devops, terraform, infrastructure-as-code, gcp, devsecops, 2articles1week, technical-writing-1, devops-articles, terraform-state, terraform-cloud, infrastructure-management, terraform-aws-infrastructureascode-provisioning-automation-cloudcomputing

---

In the previous parts of the Terraform series we had discussed about each and every important topic of Terraform along with all the popular commands that are used in the terraform for the configuration management.

So, in this part of the terraform series we will be discussing about one of the example of terraform in which we will be going to initialize the AWS EC2 instance with the Security Group & User Data using Terraform.

Since, we are provisioning the AWS EC2 instance. So, that means will be using the AWS provider.

Let's Go....

```plaintext
// AWS provider details
provider "aws" {
  region = "ap-south-1"  # AWS region
}

# Creation of the security group
resource "aws_security_group" "instance_sg" {
  name        = "instance_sg"
  description = "Security group for EC2 instance"
  
  # Inbound rules defining
  ingress {
    from_port   = 22
    to_port     = 22
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
    from_port   = 443
    to_port     = 443
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  # Outbound rules defining it allows all traffic
  egress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
  }
}

# Creation of an EC2 instance
resource "aws_instance" "example_name" {
  ami             = "ami-8548388tyre911"  # AMI id here
  instance_type   = "t2.large"  # instance type
  key_name        = "your-key-pair"  # EC2 key pair name
  security_groups = [aws_security_group.instance_sg.name]

  # the User data that are to be executed during the creation of EC2 instance
  user_data = <<-EOF
              #!/bin/bash
              sudo su
              sudo apt update
              sudo apt install -y httpd
              sudo chkconfig httpd on
              sudo systemctl start httpd
              echo "Hello from user data!" > /tmp/user_data_output.txt
              EOF
  
  tags = {
    Name = "ExampleInstance"
  }
}

output "instance_public_ip" {
  value = aws_instance.example.public_ip
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
    
3. Run `terraform plan` command to see what Terraform is planning to do upon running the apply command:
    
    ```powershell
    terraform plan
    ```
    
4. Run `terraform apply` command to apply the changes and create the EC2 instance, security group, etc:
    
    ```powershell
    terraform apply --auto-approve
    ```
    
5. And once the EC2 instance and other resources are created, we can simply SSH into it using the key pair we specified above.
    
6. To access the instance's console output, you can use the AWS Management Console:
    
    * Go to the EC2 dashboard.
        
    * Select the instance you created.
        
    * Go to the "Actions" dropdown menu and select "Instance Settings" &gt; "Get System Log".
        

This will display the console output of the instance, including the output from the user data script executed during launch.

7. You can see above in the Code of terraform that upon the creation of EC2 instance the `terraform apply` will also throw the Public IP of EC2 instance after the successful execution as an Output like:
    
    ```powershell
     Outputs:
     instance_public_ip = "31.14.168.300"
    ```
    
8. And once we are done with our work we will now destroy all the resources that we had created:
    
    ```powershell
    terraform destroy --auto-approve
    ```
    
    This command will remove all the resources created by Terraform.
    

*<mark>&lt;-- In this part we created the AWS EC2 instance, Security Group and the User Data using Terraform --&gt;</mark>*

*<mark>&lt;-- In the next part of Terraform Series we will see the another example of Terraform. --&gt;</mark>*