---
title: "Must-known Port Numbers in DevOps"
datePublished: Thu Apr 11 2024 07:18:14 GMT+0000 (Coordinated Universal Time)
cuid: cluuwqp26000n08l4eb981hyr
slug: must-known-port-numbers-in-devops
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1712816400007/3160488b-b223-46b3-bbe0-85bc346f4191.jpeg
tags: cloud, blogging, aws, azure, devops, networking, gcp, devsecops, 2articles1week, technical-writing-1, devops-articles, devops-trends, devops-journey, devopscommunity, devops-devopsarticles-devopstools-aws-amazonwebservices-terraform-kubernetes-ansible-git-d0cker-jenkins-prometheus-splunk-grafana-nagios

---

The term "ports" in DevOps frequently refers to the particular network ports that are utilized for system-wide communication between various services or components. In order to facilitate smooth communication between different components of an application or infrastructure, these ports are essential. Nevertheless, not every DevOps arrangement uses the same amount of ports; this varies widely based on the particular design, technology, and system needs. Understanding network protocols and the port numbers that correspond with them is essential for DevOps professionals to ensure effective communication across different infrastructure components. Deploying apps, administering containers, and coordinating cloud resources may all be made more efficient and secure by understanding which ports to open and how to use them.

---

# What is a Port?

A port is a communication route or logical endpoint on a host or server that is used to identify a particular activity or service. A network, like the internet, may be used to transit data between applications or services by using ports, which are a component of the addressing information.  

### Some commonly used ports in DevOps are as follows:

1. `Port Number: 443`
    
    > 1. Protocol: **HTTPS (HTTP Secure)**
    >     
    > 
    > 2. Usage: It is used for encrypting the web traffic for the enhancement of security.
    >     
    > 3. For Example: It is used for securing the online transactions on websites like e-commerce platforms.
    >     
    
2. `Port Number: 80`
    
    > 1. Protocol: **HTTP (Hypertext Transfer Protocol)**
    >     
    > 
    > 2. Usage: It is a standard port for unencrypted web traffic.
    >     
    > 
    > 3. For Example: Hosting web applications that are accessible via web browsers.
    >     
    
3. `Port Number: 22`
    
    > 1. Protocol: **SSH (Secure Shell)**
    >     
    > 2. Usage: Secure remote access to the Servers.
    >     
    > 3. For Example: Managing server configurations via using SSH (Secure Shell).
    >     
    
4. `Port Number: 9000`
    
    > 1. Protocol: Custom Application Port
    >     
    > 2. Usage: Varies based on application (e.g., Jenkins, SonarQube, Grafana).
    >     
    > 3. For Example: For Accessing SonarQube on the Web Browser.
    >     
    
5. `Port Number: 8080`
    
    > 1. Protocol: Alternative for the *HTTP or for accessing Jenkins.*
    >     
    > 2. Usage: It is used for the Proxy and Caching purposes.
    >     
    > 3. For Example: It is used for testing web applications on a development server or else it can be used for accessing the Jenkins on web browser.
    >     
    
6. `Port Number: 9090`
    
    > 1. Protocol: *Custom Application Port or Prometheus Server.*
    >     
    > 2. Usage: It is used for accessing a Monitoring tool for collection of metrics.
    >     
    > 3. For Example: It is used for Visualizing the server's performance metrics by using the Prometheus.
    >     
    
7. `Port Number: 9100`
    
    > 1. Protocol: *Node Exporter type service.*
    >     
    > 2. Usage: It is used for the collection of system-level metrics.
    >     
    > 3. For Example: It is used for Monitoring the CPU and memory usage on the target hosts.
    >     
    
8. `Port Number: 3000`
    
    > 1. Protocol: *Custom Application Port or Grafana Server.*
    >     
    > 2. Usage: It is used for accessing a Monitoring tool for visualizing the Dashboards.
    >     
    > 3. For Example: It is used for Visualizing the server's performance in the form of Dashboards by using the Grafana.
    >     
    
9. `Port Number: 9092`
    
    > 1. Protocol: *Kafka Broker.*
    >     
    > 2. Usage: It is used for the real-time data streaming and message queuing.
    >     
    > 3. For Example: It is used for Implementing message queues for the specific kind of event processing.
    >     
    
10. `Port Number: 5000`
    
    > 1. Protocol: *Docker Registry.*
    >     
    > 2. Usage: It is used for the Distribution of Docker images.
    >     
    > 3. For Example: It is used in pushing and pulling Docker images from registries like Docker Hub.
    >     
    
11. `Port Number: 2375`
    
    > 1. Protocol: *Docker Remote API.*
    >     
    > 2. Usage: It is used for Remote management of Docker Containers.
    >     
    > 3. For Example: It is used for automating the process of Docker Container deployment by using the Docker Remote API.
    >     
    
12. `Port Number: 27017`
    
    > 1. Protocol: *MongoDB Database System.*
    >     
    > 2. Usage: It is a default port for accessing the MongoDB database connections.
    >     
    > 3. For Example: It is used for storing the JSON documents in the MongoDB database.
    >     
    
13. `Port Number: 6379`
    
    > 1. Protocol: *Redis Server.*
    >     
    > 2. Usage: It is used for caching and session management.
    >     
    > 3. For Example: It is used for utilizing the Redis for caching the frequently accessed data.
    >     
    
14. `Port Number: 3306`
    
    > 1. Protocol: *MySQL Database System.*
    >     
    > 2. Usage: It is used for managing the MySQL database connections.
    >     
    > 3. For Example: It is used for hosting websites with MySQL as a Backend Service.
    >     
    
15. `Port Number: 5432`
    
    > 1. Protocol: *PostgreSQL Database System.*
    >     
    > 2. Usage: It is a default port for PostgreSQL database connections.
    >     
    > 3. For Example: It is used for storing the application's data in the PostgreSQL database.
    >     
    
16. `Port Number: 8081`
    
    > 1. Protocol: For accessing the Nexus Repository or other Custom Applications.
    >     
    > 2. Usage: It is used for the Artifactory Management.
    >     
    > 3. For Example: It is used for accessing the Nexus Repository on the Web Browser.
    >     
    
17. `Port Number: 8082`
    
    > 1. Protocol: For accessing the jFrog Artifactory or other Custom Applications.
    >     
    > 2. Usage: It is used for the Artifactory Management.
    >     
    > 3. For Example: It is used for accessing the jFrog Artifactory on the Web Browser. Though, the jFrog Artifactory can also be accessible on **8046, 8047, 8049, and 8091 ports.**
    >     
    

***<mark>-&gt; Here are some of the most commonly used Ports in DevOps.</mark>***

---

### Some more other Ports that are used in the DevOps for performing the various operations are as follows:

1. GitLab - Port 80 or 443 (HTTP/HTTPS)
    
2. Docker - Port 2375 (unencrypted) or 2376 (encrypted)
    
3. Kubernetes - Port 6443 (API server)
    
4. Ansible - Port 22 (SSH)
    
5. Terraform - No specific port (uses various APIs)
    
6. ELK Stack (Elasticsearch, Logstash, Kibana) - Elasticsearch: 9200/9300, Logstash: 5044, Kibana: 5601
    
7. Nagios - Port 5666 (NRPE)
    
8. Consul - Port 8500 (HTTP)
    
9. Puppet - Port 8140 (default)
    
10. Vagrant - No specific port (manages virtual machines)
    
11. SaltStack - Port 4505-4506 (default)
    
12. Jenkins X - Port 80 or 443 (HTTP/HTTPS)
    
13. JIRA - Port 8080 (default)
    
14. Bitbucket - Port 7990 (default)
    
15. GitLab CI/CD - Port 80 or 443 (HTTP/HTTPS)
    
16. CircleCI - No specific port (SaaS)
    
17. Travis CI - No specific port (SaaS)
    
18. TeamCity - Port 8111 (default)
    
19. Octopus Deploy - Port 10933 (default)
    
20. Chef - Port 443 (default)
    
21. Argo CD - Port 8080 (default) or else 8081
    
22. Harbor - Port 80 or 443 (HTTP/HTTPS)
    
23. Jenkins Configuration as Code (JCasC) - Port 8080 (default)
    
24. Drone - Port 8080 (default)
    
25. Spinnaker - Port 8084 (default)
    
26. CloudBees - Port 80 or 443 (HTTP/HTTPS)
    

**<mark>Note:- All the default ports can be changed just by following the certain steps.</mark>**