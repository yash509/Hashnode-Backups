---
title: "Deep Dive into Terraform - P1"
datePublished: Sun Mar 31 2024 00:30:15 GMT+0000 (Coordinated Universal Time)
cuid: cluesbnme000608l1acj6gqfn
slug: deep-dive-into-terraform-p1
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1711793422149/738efb5f-8b39-4cbe-af75-19bafd53a454.png
tags: blogging, devops, terraform, infrastructure-as-code, devsecops, 2articles1week, technical-writing-1, terraform-cloud, infrastructure-management, terragrunt, terraformworkspace

---

Nowadays, management of the infrastructure is one the mandatory requirements for the today's modernized applications like today even in the serverless environments, there are many components that requires the involvement of users for the infrastructure management.

It is unable to keep up with the rapid development cycles with manual infrastructure management. If whole infrastructure management done manually then it will simply create the huge time delays in the software or the other service delivery process.

So, to overcome this issue of doing infrastructure management manually here comes the Infrastructure as Code (IaC) that has become the solution to this issue by allowing the users to keep track of infrastructure changes along with the development. It also leads to the faster automated changes by codifying all the infrastructure and its configuration by managing them through the delivery pipeline.

Terraform is one of the leading platform to be used as Infrastructure as Code (IaC) tools that allow users to define and manage infrastructure as code.

So, before moving ahead let's take the quick overview on "What is Infrastructure as Code (IaC)".

# **What is Infrastructure as Code (IaC)?**

Terraform is an open-source infrastructure as code tool that supports multiple cloud providers and on-premises infrastructure the Infrastructure as a Code (IaC) has brought up a new approach for managing and provisioning IT infrastructure with the help of code the Infrastructure as a Code (IaC) brings automation, consistency, and scalability to infrastructure deployment and in the management of IT infrastructure. Basically, the Infrastructure as Code (IaC) is a sort of a method used in the field of cloud computing and the software development that enables the management and provision of computing infrastructure by writing and using a machine-readable script files, rather than performing the manual processes.

The Infrastructure as a Code (IaC) involves the defining of various infrastructure elements such as virtual machines, networks, storage, and configurations by using code, which can be written in the declarative programming language. This code can be stored in version control systems (VCS) like Git, which will allow the teams to do collaboration, track various changes, and roll back to previous versions if necessary. By using Infrastructure as a Code (IaC) for writing the infrastructure, the organizations or the individuals can automate the provisioning and management of various resources, by reducing the risk of errors.

Implementation of Infrastructure as Code (IaC) requires the combination of various tools and processes within a organization. The teams in the organization should select the appropriate Infrastructure as Code (IaC) tools based on their specific needs and infrastructure environment. Moreover, adopting Infrastructure as a Code (IaC) often involves the principles such as version control, automation, and the collaboration.

---

# What is Terraform?

Terraform is an open-source infrastructure as a code tool from HashiCorp. It allows users to define both on-premises and cloud resources in human-readable configuration files that can be easily versioned, reused, and shared. It transforms the way for the companies or the users to manage and deploy their infrastructure over the cloud environments. With the rise in the popularity of Terraform, it has become famous for it's efficiency, scalability, and flexibility in the world cloud computing or the cloud infrastructure environments.

The terraform is not capable of managing low-level components like webservers, storage services, and networking resources but it is also capable in managing the high-level resources such as DNS, PaaS, and SaaS components.

The terraform is a declarative tool which is used for simplifying the user's experience by allowing the users to specify the expected state of the resources without the need to specify the exact steps to achieve the desired state of infrastructure resources. Terraform let the users to define their desired cloud infrastructure using a declarative configuration language, which enables the users to define the desired states of their desired resources across various cloud providers such as Amazon Web Services (AWS), Microsoft Azure, and Google Cloud Platform (GCP).

The terraform is also capable to manage how the cloud's infrastructure needs to be modified is such a way to achieve the desired result as by the user. The terraform enables teams to use the version control systems like Git, which enables the collaboration, reproducibility, and auditability of cloud's infrastructure changes. This modernized way of codifying the cloud infrastructure not only enhances visibility and control but also promotes best practices such as code review and automated testing, which will simply leads to the improvement of overall reliability and stability of infrastructure.

Moreover, the Terraform is sort of a platform-agnostic tool, that means it can be used across any supported provider. Terraform accomplishes this by interacting with the APIs of cloud providers. When a configuration is done through Terraform, it will communicate with the necessary platform via the API and ensure the defined changes are carried out in the targeted platform and these platforms can be like Amazon Web Services (AWS), Microsoft Azure, and Google Cloud Platform (GCP). With more than 1,700 providers from HashiCorp and the Terraform community available with the Terraform Registry. Along with the configuring of resources from leading cloud providers like Azure, AWS, GCP, Oracle Cloud, etc to domain-specific platforms like Cloudflare, Datadog, and Kubernetes, etc.

## Workflow of Terraform

![Terraform Workflow (write->plan->apply) - DEV Community](https://res.cloudinary.com/practicaldev/image/fetch/s--c3DVILci--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/uploads/articles/g1ormw9rdlb77vosclve.jpeg align="left")

The workflow of Terraform is the most simplest workflow you have ever seen. As it only consists of three steps to manage any kind of infrastructure. It provides users or the organizations to change the workflow which will directly support their exact implementation needs.

1. Write: The first stage of the workflow is "Write". It is where the users creates the configurations to define the resources. It can be as simple as provisioning a simple compute instance in a particular cloud provider. This writing part can be facilitated through the HashiCorp Configuration Language (HCL) which is the default language to define or to provision the resources. Either a user can use the Cloud Development Kit for Terraform (CDKTF) which allows users to define resources using any supported common programming languages like Python, Typescript, etc.
    
2. Plan: This is the second stage of the workflow where Terraform will look at the configuration files and create an execution plan. It enables the users to see what new resources are getting created, resourced, modified, and deleted.
    
3. Apply: This is the final stage of the workflow which only takes place if the plan is accurate and once the user has confirmed the changes. The terraform will carry out the changes to achieve the desired state in a specific order along with all the resource's needs and dependencies. Terraform uses the state to keep track of all the changes to the infrastructure. It will then create a state file at the initial execution and subsequently updates the state file automatically with the new changes the terraform always uses this references this state file to identify the resources it manages and keep track of all the potential changes that are made to the infrastructure.
    

## Benefits of Terraform

1. Infrastructure as Code (IaC): The terraform allows a user to define infrastructure as code using a declarative configuration language. This approach provides various advantages such as repeatability, consistency, and the ability to track changes that are made over the time using version control systems like Git.
    
2. Platform Independent: Most of the Infrastructure as Code (IaC) tools like AWS CloudFormation and Azure Resource templates are platform specific. But, Terraform allows users to use a single tool to manage infrastructure across platforms with applications by using many tools, platforms, and multi-cloud architectures.
    
3. Modularity: The terraform use a modern design by allowing the users to create the reusable infrastructure components known as modules. And these modules can use the very common infrastructure patterns, which makes it easy to share, reuse, and manage the complex architectures.
    
4. Increased Reusability of Configurations: The terraform facilitates the creation of reusable configuration files where the users can use the same configuration files to provision the multiple environments again and again.
    
5. Higher Scalability: The terraform is designed in such a way to make it easy to scale the infrastructure needs as per requirements, from managing a small development environment to the large scale production deployments.
    
6. Community and Ecosystem: The terraform has a large community of users, contributors, and module developers who actively shares the best terraform practices, provides great support, and contribute to the growth of the infrastructure as Code (IaC) ecosystem. In terraform the Terraform Registry is like a repository for modules, providers, and other extensions, making it easy to discover and reuse the solutions.
    
7. Integration with CI/CD Pipelines: The terraform can be integrated with the popular CI/CD tools like Jenkins, GitLab CI, and CircleCI which enables a user to introduce the infrastructure changes into the software deliveries and the other related workflows. The terraform provides a simple three-step workflow that can be used for the easy integration into any CI/CD pipeline. It helps to completely automate the infrastructure management.
    

*<mark>&lt;-- So, this is basic introduction to the Terraform a Infrastructure as Code (IaC) tool. In the next part, of the Terraform Series we will be discussing about the basic commands that are used in the Terraform along with the various competitors of Terraform, and moreover we will see the commands to install terraform on the Operating System like Windows, Linux, Ubuntu, etc. --&gt;</mark>*