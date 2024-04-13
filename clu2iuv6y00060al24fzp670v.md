---
title: "Let's dive into Ansible - P3"
datePublished: Fri Mar 22 2024 10:32:01 GMT+0000 (Coordinated Universal Time)
cuid: clu2iuv6y00060al24fzp670v
slug: lets-dive-into-ansible-p3
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1711098604053/c0dff37e-487e-471f-9919-9610c577af78.png
tags: cloud, aws, azure, ansible, automation, devops, gcp, devsecops, infrastructure-management

---

As we discussed in P1 that, the Ansible is an open-source automation platform designed for managing, configuring, and deploying software and IT infrastructure. It simplifies complex tasks by providing a simple yet powerful framework for automating the tasks, such as software provisioning, configuration management, application deployment, etc. Ansible is one of the most used tools for managing cloud and on-premises infrastructure. Ansible's simplicity, scalability, and versatility make it a popular choice for automating infrastructure management tasks in both small-scale environments and large-scale enterprise deployments. Ansible's extensive library of modules allows for integration with various technologies and services, facilitating automation across diverse environments. With its intuitive syntax, robust features, and strong community support, Ansible has become a cornerstone tool for automating infrastructure management tasks in modern IT environments. Ansible is backed by RedHat and open source community.

And in P2 we discussed about the Ansible Inventory which is the collection of the machines that we would like to manage. Usually, the default location for inventory is `/etc/ansible/hosts` but we can also define a custom one in any directory. Also in P2 we discussed about the 2 types of Ansible Commands i.e. Ad-hoc Commands and Playbook Commands.

Now, in this P3 of Ansible we will discussing about the Ansible Playbooks along with some examples as well as about the use and how use variables in Ansible along with Ansible Roles.

# What is Ansible Playbooks? (in Detail)

Ansible Playbooks are the simplest way in Ansible to automate the repeating tasks in the form of reusable and consistent configuration files. Playbooks are like the scripts defined in YAML files and contain any ordered set of steps to be executed on our managed nodes or webservers. Remember that the tasks in the Ansible Playbooks are always executed from top to bottom. As well as the minimum requirement of running the Ansible Playbook is that a playbook should be defined with the managed nodes to target and some tasks to run against them.

In Ansible Playbooks, one need to take a very good care of the indentations in the playbooks. Like in Ansible Playbooks, the data elements at the same level must share the same indentation while items that are children of other items must be indented more than their parents.

Let's see an Example to get the clear overview:

```yaml
- name: Intro to Ansible Playbooks
  hosts: all 

  tasks:
  - name: Copy file hosts with permissions
    ansible.builtin.copy:
      src: ./hosts
      dest: /tmp/hosts_backup
      mode: '0644'
  - name: Add the user 'bob'
    ansible.builtin.user:
      name: bob
    become: yes
    become_method: sudo
  - name: Upgrade all apt packages
    apt:
      force_apt_get: yes
      upgrade: dist
    become: yes
```

In the above example, we created a simple playbook named `demo_playbook.yaml` that runs against all the hosts and copies a file, creates a user, and upgrades all apt packages on the remote machines.

Now we can run the Ansible's playbook by using command:-

`$ ansible-playbook demo_playbook.yaml`

Now to validate the syntax of a playbook with by using the flag `–syntax-check`.

Another handy option that you can use is the `-C` flag to perform a dry run of the playbook’s execution.

*<mark>--&gt; Basically the Ansible Playbooks enable users to automate complex tasks and maintain consistency across their infrastructure.</mark>*

## Some Examples of Ansible Playbooks

1. Ansible playbook to install the Apache HTTP server (httpd) on remote hosts:
    
    ```yaml
    - name: Install and configure Apache HTTP server
      hosts: your_target_hosts
      become: yes  # Run tasks with root privileges
    
      tasks:
        - name: Update package cache
          package:
            name: "{{ item }}"
            state: latest
          with_items:
            - yum-utils
            - epel-release  # Install EPEL repository (optional, for CentOS/RHEL)
    
        - name: Install Apache HTTP server
          package:
            name: httpd
            state: present
    
        - name: Start Apache service and enable it on boot
          service:
            name: httpd
            state: started
            enabled: yes
    ```
    
    2. Ansible playbook for installing Apache HTTP Server on Ubuntu servers:-
        
    
    ```yaml
    - name: Install Apache HTTP Server
      hosts: webservers
      become: yes
      tasks:
        - name: Update apt package cache
          apt:
            update_cache: yes
    
        - name: Install Apache2 package
          apt:
            name: apache2
            state: present
    
        - name: Ensure Apache service is enabled and running
          service:
            name: apache2
            state: started
            enabled: yes
    ```
    
    3. Ansible playbook for installing Python 3 on remote hosts:-
        
        ```yaml
        - name: Install Python 3
          hosts: all
          become: yes
          tasks:
            - name: Update apt package cache (for Ubuntu)
              apt:
                update_cache: yes
              when: ansible_os_family == 'Debian'
        
            - name: Install Python 3 (for Ubuntu/Debian)
              apt:
                name: python3
                state: present
              when: ansible_os_family == 'Debian'
        
            - name: Install Python 3 (for CentOS/RHEL)
              yum:
                name: python3
                state: present
              when: ansible_os_family == 'RedHat'
        ```
        
    4. Ansible playbook for installing Jenkins on a target hosts:
        
        ```yaml
        - name: Install Jenkins
          hosts: your_target_host
          become: yes  # This allows the tasks to be executed with sudo privileges
        
          tasks:
            - name: Install Java
              apt:
                name: openjdk-11-jdk  # Change this according to your package manager if not using apt
                state: present
              become: yes
        
            - name: Add Jenkins repository key
              apt_key:
                url: https://pkg.jenkins.io/debian/jenkins.io.key
                state: present
        
            - name: Add Jenkins repository
              apt_repository:
                repo: deb https://pkg.jenkins.io/debian-stable binary/
                state: present
        
            - name: Install Jenkins
              apt:
                name: jenkins
                state: present
              become: yes
        
            - name: Start Jenkins service
              service:
                name: jenkins
                state: started
                enabled: yes
              become: yes
        ```
        
        *<mark>Note:- This above playbook assumes that the target host is reachable via SSH and that you have appropriate permissions to install software.</mark>*
        
    5. Ansible Playbook for installing SonarQube on the target host:
        
        ```yaml
        - name: Install SonarQube
          hosts: sonarqube_servers
          become: true
          
          tasks:
            - name: Install prerequisite packages
              package:
                name: "{{ item }}"
                state: present
              with_items:
                - wget
                - unzip
                - openjdk-11-jdk
          
            - name: Download SonarQube
              get_url:
                url: "https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-8.9.3.48735.zip"
                dest: "/tmp/sonarqube.zip"
          
            - name: Unzip SonarQube
              unarchive:
                src: "/tmp/sonarqube.zip"
                dest: "/opt/"
                remote_src: yes
          
            - name: Rename SonarQube directory
              command: mv /opt/sonarqube-* /opt/sonarqube
          
            - name: Set SonarQube directory ownership
              file:
                path: "/opt/sonarqube"
                owner: "{{ ansible_user }}"
                group: "{{ ansible_user }}"
                state: directory
          
            - name: Configure SonarQube server
              template:
                src: sonar.properties.j2
                dest: "/opt/sonarqube/conf/sonar.properties"
          
            - name: Start SonarQube service
              systemd:
                name: sonarqube
                state: started
                enabled: yes
        ```
        
        *<mark>Note:- This above playbook assumes that the target host is reachable via SSH and that you have appropriate permissions to install software.</mark>*
        
    
    So, In this way we can install various package's and software's on the webservers or hosts.
    

# Variables in Ansible

In Ansible, variables play a crucial role in making playbooks more flexible and reusable. They allow you to define values once and reference them throughout your playbook, making it easier to manage configurations and parameters. Basically, we can say that Variables can be defined in Ansible at more than one level and Ansible chooses the variable to use based on variable precedence. 

Simply we can use the common method is to use a `vars` block at the beginning of each playbook variables at the playbook level and after declaring them, we can use them in tasks by using the `{{ variable_name }}`to reference a variable in a task. For Example:

```yaml
- name: variables playbook
  hosts: all
  vars:
      state: latest 
      user: steve
  tasks:
  - name: Add the user {{ user }}
    ansible.builtin.user:
      name: "{{ user }}"
  - name: Upgrade all apt packages
    apt:
      force_apt_get: yes
      upgrade: dist
  - name: Install the {{ state }} of package "nginx"
    apt:
      name: "nginx"
      state: "{{ state }}"
```

Here in the above example we can clearly see that the we had defined 2 variables under the `vars:` one is state and the another one is user. And as we move ahead in this above playbook we can use the variables that we created above to define the values like in above scenarios. When referencing a variable as another variable’s value, we must add quotes around the values as shown in the above example.

And now we can run the above Playbook by using the command:-

`ansible-playbook variables_playbook.yaml`

# What is Ansible Roles?

Ansible roles are the ways of organizing and structuring your Ansible code in a reusable manner. Roles allow you to break down complex automation tasks into smaller, more manageable units, making your playbooks cleaner, easier to understand, and more modular. The roles can be reused across multiple playbooks and shared with the Ansible community through platforms like Ansible Galaxy. They promote code reuse, maintainability, and collaboration in Ansible projects, making it easier to manage infrastructure automation at scale. With the help of roles, you get a standardized structure for bundling related tasks, variables, templates, handlers, and files, and this enhances reusability.

Some Ansible Roles and their workings:

1. Directory Structure: Ansible roles follow a specific directory structure that helps organize your tasks, variables, templates, and other files related to the role.
    
    ```plaintext
    my_role/
    ├── defaults/
    │   └── main.yaml
    ├── files/
    ├── handlers/
    │   └── main.yaml
    ├── meta/
    │   └── main.yaml
    ├── tasks/
    │   └── main.yaml
    ├── templates/
    ├── tests/
    ├── vars/
    │   └── main.yaml
    └── README.md
    ```
    
2. Variables: The `vars` directory contains YAML files with variables specific to the role.
    
3. Files: The `files` directory contains static files that need to be copied to the remote hosts as part of the role execution.
    
4. Meta: The `meta` directory contains a `main.yaml` file with metadata about the role, such as dependencies on other roles or role-specific tags.
    
5. README.md: A README file containing documentation for the role, including usage instructions, variables descriptions, and any other relevant information.
    
6. Tests: The `tests` directory can contain test files or playbooks used to test the role's functionality.
    
7. Handlers: The `handlers` directory contains YAML files with handlers, which are tasks triggered by other tasks when certain conditions are met.
    
8. Defaults: The `defaults` directory contains a `main.yaml` file with default variable values for the role.
    
9. Tasks: The `tasks` directory contains YAML files with the main tasks to be executed by the role. These tasks can include actions like installing packages, copying files, etc.
    
10. Templates: The `templates` directory contains Jinja2 templates that can be used to dynamically generate configuration files or scripts and these templates can include variables.
    

*!--- So, now this is the final part of Ansible series, and in these 3 parts of Let's Dive into Ansible series, I tried to cover the each and every important topic along with examples. In these 3 parts of Ansible we explored Ansible’s basic concepts, features, and functionalities with examples while we also explained why it is such a great tool for automation purposes. ---!*

*<mark>"Thanks for visiting"</mark>*