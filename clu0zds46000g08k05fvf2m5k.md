---
title: "Let's dive into Ansible (Introduction) - P1"
datePublished: Thu Mar 21 2024 08:39:05 GMT+0000 (Coordinated Universal Time)
cuid: clu0zds46000g08k05fvf2m5k
slug: lets-dive-into-ansible-introduction-p1
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1711005994339/e0ad9fce-8cbc-4f86-a712-ecd8dbd75fd5.png
tags: cloud, ansible, devops, devsecops, infrastructure-management

---

# What is Ansible?

Ansible is an open-source automation platform designed for managing, configuring, and deploying software and IT infrastructure. It simplifies complex tasks by providing a simple yet powerful framework for automating the tasks, such as software provisioning, configuration management, application deployment, etc. Ansible is one of the most used tools for managing cloud and on-premises infrastructure. Ansible's simplicity, scalability, and versatility make it a popular choice for automating infrastructure management tasks in both small-scale environments and large-scale enterprise deployments. Ansible's extensive library of modules allows for integration with various technologies and services, facilitating automation across diverse environments. With its intuitive syntax, robust features, and strong community support, Ansible has become a cornerstone tool for automating infrastructure management tasks in modern IT environments. Ansible is backed by RedHat and open source community.

# How the Ansible works?

See, the Ansible operates on a client-server architecture, where the control node manages the configuration and automation tasks across remote hosts. Basically, Ansible uses the concepts of control and managed nodes. The control node, or a developer's machine, executes Ansible commands and playbooks for configuring and managing the infrastructure. And the Managed Nodes, are responsible for sending the commands and various instructions.

When a user runs the Ansible commands or playbooks, the control node sends the necessary instructions to the remote hosts, which will then executes the specified tasks. These tasks are defined within YAML playbooks. Each task in a playbook corresponds to a specific action, such as installing packages, configuring files, or starting services, etc.

The ansible's execution model usually follows the push-based approach, meaning that the control node initiates communication with the remote hosts to enforce the desired state defined in the playbooks. The ansible also employs a very strict execution strategy by ensuring that running the same ansible playbooks multiple times gives consistent results, even in the exposure of complex environments.

As discussed earlier that the ansible uses a very simple human readable language i.e. YAML to define or to create the ansible playbooks. You can't even imagine that the YAML based ansible playbooks are really easy to understand and to write.

Apart from these stuffs the Ansible doesn’t require the installation of any extra agents on the managed nodes so it is absolutely simple to start using it. Only the user or a developer needs is a terminal to execute Ansible commands and a text editor to define the configuration files or playbooks.

Overall, Ansible is a combination of agentless architecture, YAML-based playbooks, and push-based execution model provides a straightforward and efficient means of automating infrastructure management tasks across the various IT environments.

# Benefits of Ansible

1. Easy to start and use from day one, without the need for any special coding skills.
    
2. A free and open-source community project with a very large amount of audience or community.
    
3. Deployment is very easy, that means anyone can you it.
    
4. Ansible's simple YAML syntax and agentless architecture make it easy to learn, deploy, and manage.
    
5. Ansible has a good scalability that means it scales efficiently to manage infrastructure of any size, from small environments to the large-scale deployments.
    
6. Ansible automates tasks, thus reducing the manual works and that leads to minimizing the human error.
    

# Some Basic terms used in Ansible

1. Playbook: A YAML file that defines a set of tasks to be executed on remote hosts.
    
2. Task: A single unit of work defined within a playbook.
    
3. Module: Pre-built units of code that Ansible uses to perform tasks on remote hosts.
    
4. Play: It is a combination of one or more plays within a playbook. Each play consists of a list of tasks and defines a set of hosts on which those tasks will going to be executed.
    
5. Inventory: A list of managed hosts that Ansible will operate on. It could be a static file in the simple cases or else we can pull the inventory from remote sources, such as cloud providers (AWS, GCP and Azure).
    
6. Roles: They are the reusable collection of playbooks, variables, and other Ansible components that organize tasks and configurations into logical units.
    
7. YAML: A popular and simple data format that is very clean and understandable by humans.
    
8. Groups: They are the several hosts grouped together that share a common attribute.
    
9. Facts: These are the information gathered by Ansible about managed hosts, such as OS details, network interfaces, etc.
    

# How to install Ansible

To install the Ansible you can follow these steps:

1. Checking your System's Requirements: Do ensure that you meet the system requirements for installing Ansible. Ansible can be installed on various operating systems including Linux, macOS, and Windows Subsystem for Linux (WSL). Additionally, also make sure that you have Python installed because Ansible is written in Python.
    
2. Choosing the Installation Method: There are several methods to install Ansible
    
    <mark>a.</mark> Using Linux Package Manager: For Debian/Ubuntu you can use "apt" -
    
    `Commands: sudo apt update -y`
    
    `sudo apt install ansible -y`
    
    <mark>b.</mark> Using Python pip: You can install Ansible via Python's package manager, pip.
    
    `Command: pip install ansible`
    
    <mark>c.</mark> For macOS (Package Manager): If you're using macOS, you can install Ansible via Homebrew
    
    `Command: brew install ansible`
    
    <mark>d.</mark> For Windows (Package Manager): If you're using Windows Subsystem for Linux (WSL), you can install Ansible via the package manager of your Linux distribution.
    
3. Verify the Installation: You can verify that if Ansible is installed correctly by checking its version by using:
    
    `Command: ansible --version`
    
4. Setting up the SSH Keys: If you plan to manage remote hosts using Ansible, it's recommended to set up SSH keys for password less authentication. <mark>(though it is completely optional)</mark>
    
5. Setting up the Configurations: Ansible can be configured via the `ansible.cfg` file, which allows you to specify settings such as default inventory location, module paths, and more. By default, Ansible will look for the configuration file in the path `/etc/ansible/ansible.cfg.`<mark>(it is also optional)</mark>
    
      
    
    ***\--&gt; Once you've completed these above steps, Ansible should be installed and ready to use on your system. And now, you can start writing playbooks and managing your infrastructure using Ansible's powerful automation capabilities.***