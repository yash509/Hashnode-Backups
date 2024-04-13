---
title: "Deep Dive into Terraform - P2 
(Terraform Commands and Installation)"
datePublished: Mon Apr 01 2024 00:30:22 GMT+0000 (Coordinated Universal Time)
cuid: clug7rnox000008l4hgw81nm8
slug: deep-dive-into-terraform-p2-terraform-commands-and-installation
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1711798385471/7dc68b83-3ee1-4ed7-b19f-063de6f0dc76.png
tags: blogging, devops, terraform, infrastructure-as-code, devsecops, 2articles1week, technical-writing-1, terraform-cloud, infrastructure-management, terragrunt, terraformworkspace

---

So, in the previous part of Terraform we discussed about the basic introduction of Terraform, Benefits of Terraform and the Workflow of Terraform. Before, moving ahead with the commands of Terraform and other related things let's take a quick overview on the Terraform basics.

# What is Terraform?

Terraform is an open-source infrastructure as code tool from HashiCorp. It allows users to define both on-premises and cloud resources in human-readable configuration files that can be easily versioned, reused, and shared. It transforms the way for the companies or the users to manage and deploy their infrastructure over the cloud environments. With the rise in the popularity of Terraform, it has become famous for it's efficiency, scalability, and flexibility in the world cloud computing or the cloud infrastructure environments.

The terraform is not capable of managing low-level components like webservers, storage services, and networking resources but it is also capable in managing the high-level resources such as DNS, PaaS, and SaaS components.

The terraform is a declarative tool which is used for simplifying the user's experience by allowing the users to specify the expected state of the resources without the need to specify the exact steps to achieve the desired state of infrastructure resources. Terraform let the users to define their desired cloud infrastructure using a declarative configuration language, which enables the users to define the desired states of their desired resources across various cloud providers such as Amazon Web Services (AWS), Microsoft Azure, and Google Cloud Platform (GCP).

---

# Terraform Commands

1. `terraform init` **:-** The `terraform init` command is used to Initialize the new or existing Terraform working directory by downloading the required provider plugins and sets up the backend to store the state file of terraform. This is the first command that is to be executed before running any other Terraform command.
    
2. `terraform plan` :- The `terraform plan` command is used to view the changes that the Terraform will make to the infrastructure in order to get the desired state, without making any sort of changes. This command is highly useful to see what changes does the Terraform will going make before applying them. It does not make any changes it's just like a simple dry run.
    
3. `terraform validate` :- The `terraform validate` command is used to validate the syntax and the structure of the Terraform configuration files. This command checks for errors, missing required arguments, and other issues that are related to the Terraform configuration files. Basically, it validates the configuration files in the current directory for the syntax errors and other basic configuration errors.
    
4. `terraform apply` :- The `terraform apply` command is used to apply the changes to the infrastructure as described in the Terraform configuration files. This command will create, modify, or delete resources as needed to bring the infrastructure into the desired state. This is the next command after the `terraform plan` command that a user will run to actually make the desired changes.
    
5. `terraform fmt` :- The `terraform fmt` command is used to rewrite the Terraform configuration files into a canonical format, which makes it easier for a user to read and maintain the Terraform configuration files.
    
6. `terraform destroy` :- The `terraform destroy` command is used to destroy all the infrastructure that is created by the Terraform, by freeing up resources and ensuring that you’re not paying for unused infrastructure. This command should be used with caution as it will delete all the resources described in the configuration file. Basically, it destroys all the resources defined in the configuration files, by effectively deleting all the infrastructure managed by the Terraform.
    
7. `terraform import` :- The `terraform import` command is used to import the existing infrastructure into your Terraform state. Overall, It allows you to bring the existing resources under Terraform management without recreating them.
    
8. `terraform output` :- The `terraform output` command is used to extract the outputs from the Terraform state files and it displays the output values defined in your Terraform configuration files.
    
9. `terraform state` :- The `terraform state` command is used to inspect and manage Terraform state files. You can use it to manually modify the state, move resources between states, and perform various other state-related operations.
    
10. `terraform refresh` :- The `terraform refresh` command is used to update the Terraform state file with the real-world infrastructure. It queries the current state of the resources and updates the Terraform state file accordingly.
    
11. `terraform taint` :- This `terraform taint` command is used to mark the resource for recreation if needed. It forces the Terraform to destroy and recreate the specified resource during the next `terraform apply`.
    
12. `terraform untaint` :- This `terraform untaint` command is used to remove all the "tainted" state from the resource. Once untainted, the terraform will again start managing the resource normally.
    
13. `terraform init -upgrade` :- The `terraform init -upgrade` command is used tp upgrade the configurations to the latest version of Terraform. It is very useful if you have recently upgraded your Terraform version and want to ensure that your configuration is compatible with the new version or not.
    
14. `terraform graph` :- The `terraform graph` command is used to generate the visual representation of the dependency graph between resources defined in your Terraform configuration files.
    
15. `terraform --version` :- The `terraform --version` command is used to check the current version of Terraform.
    

---

# **Competitors of Terraform**

1. Ansible:- Ansible is an open-source automation platform designed for managing, configuring, and deploying software and IT infrastructure. It simplifies complex tasks by providing a simple yet powerful framework for automating the tasks, such as software provisioning, configuration management, application deployment, etc. Ansible is one of the most used tools for managing cloud and on-premises infrastructure. Ansible's simplicity, scalability, and versatility make it a popular choice for automating infrastructure management tasks in both small-scale environments and large-scale enterprise deployments. Ansible's extensive library of modules allows for integration with various technologies and services, facilitating automation across diverse environments. With its intuitive syntax, robust features, and strong community support, Ansible has become a cornerstone tool for automating infrastructure management tasks in modern IT environments. Ansible is backed by RedHat and open source community.
    
2. AWS CloudFormation:- AWS CloudFormation is an infrastructure as code (IaC) tool provided by Amazon Web Services (AWS). It allows users to define and manage infrastructure resources in a declarative way using JSON or YAML templates. CloudFormation supports a wide range of AWS services and is tightly integrated with other various AWS tools and services.
    
3. Puppet: Puppet is another open-source infrastructure as code (IaC) tool that uses a declarative language to define and manage infrastructure resources.
    
4. Chef**:** Chef is an open-source infrastructure as code (IaC) tool that uses Ruby scripts to define and manage infrastructure resources. Chef is generally used for managing the large-scale infrastructures and it also supports the wide range of platforms and various cloud providers.
    
5. Kubernetes**:** The Kubernetes also works as an alternative to Terraform. As, it is an open-source tools that enables the automated deployment, management, and scaling of containerized applications.
    

---

# Terraform Installation

### **Step 1: Download Terraform**

1. Go to the [Terraform downloads](https://developer.hashicorp.com/terraform/install) page in your web browser.
    
2. Identify the version of Terraform suitable for your OS. Choose the version based on your system architecture (example:- 32-bit or 64-bit).
    
3. Right-click on the download link for your OS and select "Copy link address" or on some other similar kind of option to copy the URL to the Terraform binary file.
    

### **Step 2: Install Terraform**

#### For Linux/macOS:

1. Open your terminal.
    
2. Change directory to a location where you stored your Terraform file. For example:
    
    ```yaml
    cd Downloads/
    ```
    
3. Download Terraform using the `curl` command. Replace `<URL>` with the link address that you had copied in the 3rd part of 1st Step:
    
    ```yaml
    curl -O <URL>
    ```
    
4. Now, extract the downloaded file:
    
    ```yaml
    unzip terraform*.zip
    ```
    
5. Move the extracted binary to a directory included in your system's PATH. For example:
    
    ```yaml
    sudo mv terraform /usr/local/bin/
    ```
    

#### For Windows:

1. Open your web browser and navigate to the [URL](https://developer.hashicorp.com/terraform/install).
    
2. Download the Terraform zip file for Windows.
    
3. Extract the downloaded zip file.
    
4. Move the extracted `terraform.exe` file to a directory included in your system's PATH.
    

### **Step 3: Verify Installation**

After installing Terraform, in both the cases of Windows and LInux/macOS you can verify that whether the installation is successful or not by running the below command in your terminal or in the command prompt:

```yaml
terraform version
```

---

*<mark>&lt;-- So, in this part of Terraform we discussed about the various Terraform Commands, Competitors of Terraform and How to install Terraform both in Windows and Linux and macOS. --&gt;</mark>*

*<mark>&lt;-- In the next part, of the Terraform Series we will be discussing about the Terraform State File, about various ways to store the Terraform State File in a secured way. As the safe storing of Terraform State File is one of the good practices that a DevOps Engineer can follow. As the Terraform State File contains the important as well as the confidential information about the infrastructure in deep and the credentials of the account where the deployments took place using </mark>* <mark>Infrastructure as code (IaC)</mark>*<mark>. --&gt;</mark>*