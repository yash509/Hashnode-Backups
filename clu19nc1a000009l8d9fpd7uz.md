---
title: "Let's dive into Ansible - P2"
datePublished: Thu Mar 21 2024 13:26:27 GMT+0000 (Coordinated Universal Time)
cuid: clu19nc1a000009l8d9fpd7uz
slug: lets-dive-into-ansible-p2
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1711024046750/09345dac-5ecc-4857-9f17-b797f9934cd9.png
tags: cloud, ansible, devops, devsecops, infrastructure-management, ansible-playbook

---

As we discussed earlier that, the Ansible is an open-source automation platform designed for managing, configuring, and deploying software and IT infrastructure. It simplifies complex tasks by providing a simple yet powerful framework for automating the tasks, such as software provisioning, configuration management, application deployment, etc. Ansible is one of the most used tools for managing cloud and on-premises infrastructure. Ansible's simplicity, scalability, and versatility make it a popular choice for automating infrastructure management tasks in both small-scale environments and large-scale enterprise deployments. Ansible's extensive library of modules allows for integration with various technologies and services, facilitating automation across diverse environments. With its intuitive syntax, robust features, and strong community support, Ansible has become a cornerstone tool for automating infrastructure management tasks in modern IT environments. Ansible is backed by RedHat and open source community.

So, in this part we will be understanding the various other concepts used in Ansible.

# What is Ansible Inventory? (in Detail)

As told earlier, the inventory is the collection of the machines that we would like to manage. Usually, the default location for inventory is `/etc/ansible/hosts` but we can also define a custom one in any directory. Basically, in ansible the inventory is a file or directory structure containing information about the hosts or nodes that Ansible will manage. The inventory file is where you define the hosts and groups of hosts that Ansible can connect to and execute tasks on. It can be written in INI-style or YAML format, although YAML is more flexible and powerful.

A Inventory file includes:-

1. Hosts: These are the individual machines or servers that Ansible will interact with. Each host entry includes an IP address.
    
2. Groups: Hosts can be organized into groups, which allow you to execute tasks on multiple hosts simultaneously or define common configurations for groups of hosts.
    
3. Meta Information: Additionally to the basic host and group information, the inventory file can include aliases, SSH port information, and other meta-information needed for connecting hosts or the management of the hosts.
    
4. Variables: You can assign variables to individual hosts or groups, which will allow you to customize configurations or tasks based on a particular set of criteria.
    

As we discussed that the Ansible Inventory files can be written in either YAML format or in INI format. Basically, the term INI is a short form of the Ansible INI inventory plugin. The plugin uses an Ansible INI file as an inventory source and is part of `ansible-core`. The full name of the plugin is `ansible.builtin.ini`

<mark>The example of an Ansible inventory file in INI format:</mark>

```ini
[webservers]
web1.example.com
web2.example.com
web3.example.com

[databases]
db1.example.com
db2.example.com
db3.example.com

[loadbalancers]
lb1.example.com
lb2.example.com

[all:vars]
ansible_user=admin
```

<mark>The same example of an Ansible inventory file in YAML format:</mark>

```yaml
all:
  vars:
    ansible_user: admin
  children:
    webservers:
      hosts:
        web1.example.com:
        web2.example.com:
        web3.example.com:
    databases:
      hosts:
        db1.example.com:
        db2.example.com:
        db3.example.com:
    loadbalancers:
      hosts:
        lb1.example.com:
        lb2.example.com:
```

You can specify the inventory file to use with Ansible by passing the `-i` flag followed by the path to the inventory file when executing Ansible commands or playbooks. Ansible also provides dynamic inventory options for fetching inventory information from external sources like cloud providers (eg:- AWS, GCP, Azure).

# Ansible Commands

There are 2 primary types of commands used in Ansible are:

1. Ad-hoc Commands
    
2. Playbook Commands
    

### Ad-hoc Commands

The Ad-hoc commands is a quick way to run a single task on one or more managed nodes. Ad-hoc commands are used for quick, one-time tasks without the need to write a playbook. These commands are executed directly from the command line and are useful for tasks like gathering information, making quick changes, or performing simple tasks across a group of hosts. Some examples of valid use cases are rebooting servers, copying files, checking connection status, etc. The syntax for Ad-hoc commands are like:

`ansible <host-pattern> -m <module> -a "<module options>"`

The term `<host-pattern>` is a thing to which the managed hosts to run against

`-m:` the module to run followed by module name

`-a:` the list of arguments required by the module

Example of Ad-hoc Command:- `ansible all -m ping`

### Playbook Commands:

Playbooks are Ansible's configuration, deployment, and orchestration language. They are written in YAML format and allow for more complex automation workflows. Playbooks can define multiple tasks, each comprising one or more than one plays, which describe a series of steps to be executed on a particular hosts. Playbooks provide more flexibility and reusability as compared to ad-hoc commands. A playbook can be used again and again and be executed on a single host or a group of hosts because of it's reusability feature. For example: Given below is a playbook that installs and starts Apache on hosts specified under the 'webservers' group in the inventory file.

```yaml
---
- name: Install and start Apache
  hosts: webservers
  tasks:
    - name: Install Apache
      yum:
        name: httpd
        state: present
    - name: Start Apache
      service:
        name: httpd
        state: started
```

These two types of commands provide different levels of control and flexibility for managing infrastructure with Ansible. Ad-hoc commands are suitable for quick tasks, while playbooks are ideal for complex automation workflows.