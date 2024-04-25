---
title: "DevSecOps Project 2: Deployment of Hotstar Clone Application"
datePublished: Thu Apr 25 2024 00:30:40 GMT+0000 (Coordinated Universal Time)
cuid: clveichud000109me4sag6o14
slug: devsecops-project-2-deployment-of-hotstar-clone-application
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1713941830798/e9e67060-560c-4113-bc33-85403887b57e.jpeg
tags: cloud, docker, aws, github, sonarqube, kubernetes, git, devops, jenkins, devsecops, technical-writing-1, devops-articles, trivy, devops-journey, devopscommunity

---

It is now essential to incorporate strong security procedures into the development pipeline due to the constantly changing nature of software development and deployment. Combining the domains of development, security, and operations, DevSecOps stresses the proactive mitigation of possible risks and vulnerabilities by integrating security measures throughout the software development lifecycle.

This blog provides a step-by-step manual for using the DevSecOps principles on Amazon Web Services (AWS) to build a popular streaming platform clone. Automation, security, and efficiency are achieved through the deployment process by leveraging a range of technologies and services such as Docker, Jenkins, Java, SonarQube, AWS CLI, Kubectl, and Terraform.

Starting the adventure involves setting up an Ubuntu-configured AWS EC2 instance and assigning it a particular IAM role to boost learning. The installation of essential tools and dependencies needed for the deployment pipeline is then accomplished automatically by a script, guaranteeing consistency and efficiency throughout the entire setup.

Jenkins jobs are used for orchestration in this DevSecOps strategy. Tasks like setting up an Amazon EKS cluster, launching the Hotstar clone application, and putting security protections in place at different deployment phases are defined at different stages and executed via these stages.

A crucial part of this approach is the incorporation of security measures. Through the use of SonarQube, OWASP, and Docker Scout, the blog will explain how security checks, container security scans, and static code analysis are all integrated into the pipeline. These safeguards provide a reliable and secure deployment by strengthening the application against potential weaknesses.

**<mark>GitHub URL</mark>**<mark>:- </mark> [<mark>https://github.com/yash509/DevSecOps-Project----Hotstar-Deployment.git</mark>](https://github.com/yash509/DevSecOps-Project----Hotstar-Deployment.git)

# Steps:-

Step 1 —&gt; Launch an Ubuntu(22.04) T2 Large Instance

Step 2 —&gt; Install Jenkins, Docker and Trivy. Create a Sonarqube Container using Docker.

Step 3 —&gt; Install Prometheus and Grafana On the new Server.

Step 4 —&gt; Install the Prometheus Plugin and Integrate it with the Prometheus server.

Step 5 —&gt; Email Integration With Jenkins and Plugin setup.

Step 6 —&gt; Install Plugins like JDK, Sonarqube Scanner, Nodejs, and OWASP Dependency Check.

Step 7 —&gt; Create a Pipeline Project in Jenkins using a Declarative Pipeline

Step 8 —&gt; Install OWASP Dependency Check Plugins

Step 9 —&gt; Install Docker Scout Docker Image Build and Push

Step 10 —&gt; Deploy the image using Docker

Step 11 —&gt; Kubernetes Master and Slave server setup on Ubuntu (20.04)

Step 12 —&gt; Terminate the AWS EC2 Instances.  

**<mark>Now, let's start implementing each step mentioned above...!!</mark>**

# **Step 1: Launch an Ubuntu(22.04) T2 Large Instance:-**

Launch an AWS t2.large Instance. Use the image as Ubuntu. You can create a new key pair or use an existing one. Enable HTTP and HTTPS settings in the Security Group and open all ports.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694159201292/35d8cf58-7ba8-4dc0-a1f8-9cc017439910.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

# **Step 2: Install Jenkins, Docker and Trivy:-**

### 2A:- Install Jenkins

```powershell
sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins

sudo apt update
sudo apt install openjdk-17-jdk
sudo apt install openjdk-17-jre

sudo systemctl enable jenkins
sudo systemctl start jenkins
sudo systemctl status jenkins
```

Once the Jenkins is installed, go to your AWS EC2 Security Group and open Inbound Port 8080, since Jenkins works on default Port 8080.

![](https://miro.medium.com/v2/resize:fit:875/0*LwcZZbzeA-C2wTqx.png align="left")

Now, copy your public IP address of your instance, and use the below command to get your password of Jenkins:-

```powershell
<EC2 Public IP Address:8080>
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

Unlock Jenkins using an administrative password and install the required plugins:-

![](https://miro.medium.com/v2/resize:fit:875/0*Kx6RTKAtbvrbb9xw.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1713506266787/ffbe1f35-58d6-442d-8dde-e46bb5fdbd7d.jpeg?auto=compress,format&format=webp align="left")

Jenkins will now get installed and install with all the libraries.

Now, Create a user, then click on save and continue.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1713506378163/48acd5fa-5323-4ea9-b3fb-244d7a247154.jpeg?auto=compress,format&format=webp align="left")

Jenkins Getting Started Screen.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1713506486530/dd5a2d42-72d2-4540-9fea-ccbbd82ec8b5.jpeg?auto=compress,format&format=webp align="left")

### 2B:- Install Docker

```powershell
sudo apt-get update
sudo apt-get install docker.io -y
sudo usermod -aG docker $USER   #my case is ubuntu
newgrp docker
sudo chmod 777 /var/run/docker.sock
```

After the docker installation, we create a SonarQube container, and do remember to add 9000 port in the security group.

![](https://miro.medium.com/v2/resize:fit:875/0*IpH7z19f_OwmC2LS.png align="left")

Now, Install SonarQube using the below command:-

```powershell
docker run -d --name sonar -p 9000:9000 sonarqube:lts-community
```

The output you will get after running the above SonarQube installation command is:-

![](https://miro.medium.com/v2/resize:fit:875/0*8xbXhpkCePWV5y9e.png align="left")

Now, you can access the SonarQube on browser like this:-

```powershell
<EC2 Public IP Address:9000>
```

Now, the SonarQube is up and running and default username and password of SonarQube is <mark>admin</mark>

![](https://miro.medium.com/v2/resize:fit:875/0*XfaIUB3jOyoVszR-.png align="left")

Enter username and password, click on login and change password:-

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1713507004497/05edea43-6e69-48d1-82b9-e9ec9b2e26a2.jpeg?auto=compress,format&format=webp align="left")

Now, after updating the New password, you can view this SonarQube dashboard:-

![](https://miro.medium.com/v2/resize:fit:875/0*yo4nGGCCWjo1RvxL.png align="left")

### 2C:- Install Trivy

```powershell
sudo apt-get install wget apt-transport-https gnupg lsb-release -y
wget -qO - https://aquasecurity.github.io/trivy-repo/deb/public.key | gpg --dearmor | sudo tee /usr/share/keyrings/trivy.gpg > /dev/null
echo "deb [signed-by=/usr/share/keyrings/trivy.gpg] https://aquasecurity.github.io/trivy-repo/deb $(lsb_release -sc) main" | sudo tee -a /etc/apt/sources.list.d/trivy.list
sudo apt-get update
sudo apt-get install trivy -y
```

# **Step 3: Install Prometheus and Grafana on the new Server**

### **3A:- Install Prometheus**

Let’s check the latest version of Prometheus from the **download page**.

You can use the curl or wget command to download Prometheus.

```powershell
wget https://github.com/prometheus/prometheus/releases/download/v2.47.1/prometheus-2.47.1.linux-amd64.tar.gz
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696600414815/73246987-a1f6-486f-b7ee-a04b93d6d6ad.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

Then, we need to extract all Prometheus files from the archive:-

```powershell
tar -xvf prometheus-2.47.1.linux-amd64.tar.gz
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696600581447/cc71be79-2302-4800-87b9-b37a56003194.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

Usually, you would have a disk mounted to the data directory. For this tutorial, I will simply create a /data directory. Also, you need a folder for Prometheus configuration files:-

```powershell
sudo mkdir -p /data /etc/prometheus
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696601423597/c114e1a6-e7c4-4b1b-b94a-acf8db788f5c.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

Now, let’s change the directory to Prometheus and move some files:-

```powershell
cd prometheus-2.47.1.linux-amd64/
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696601458188/9432c2f2-d080-4eaa-ae86-c0531f399c6a.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

First of all, let’s move the Prometheus binary and a promtool to the /usr/local/bin/. promtool is used to check configuration files and Prometheus rules:-

```powershell
sudo mv prometheus promtool /usr/local/bin/
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696601475999/49ef1753-9b35-453d-a0ec-bcc794634047.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

Optionally, we can move console libraries to the Prometheus configuration directory. Console templates allow for the creation of arbitrary consoles using the Go templating language. You don’t need to worry about it if you’re just getting started.

```powershell
sudo mv consoles/ console_libraries/ /etc/prometheus/
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696601531224/41309ace-bd16-4b18-9132-2e0d28901ff2.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

Finally, let’s move the example of the main Prometheus configuration file.

```powershell
sudo mv prometheus.yml /etc/prometheus/prometheus.yml
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696601588638/8896e4d1-c285-49ac-94c5-3c387af9046f.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

To avoid permission issues, you need to set the correct ownership for the /etc/prometheus/ and data directory:-

```powershell
sudo chown -R prometheus:prometheus /etc/prometheus/ /data/
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696601688086/3dc7c3cc-a13d-4586-87ff-f0a50cb357ee.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

Verify that you can execute the Prometheus binary by running the following command:

```powershell
prometheus --version
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696601822353/ab7b9d60-89a7-4fcd-9049-07ede5037a16.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

We’re going to use some of these options in the service definition.

We’re going to use Systemd, which is a system and service manager for Linux operating systems. For that, we need to create a Systemd unit configuration file.

```powershell
sudo vi /etc/systemd/system/prometheus.service
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696601959050/e9829329-a358-4804-b921-e2e830dcc996.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

**<mark>Prometheus.service</mark>**

```powershell
[Unit]
Description=Prometheus
Wants=network-online.target
After=network-online.target
StartLimitIntervalSec=500
StartLimitBurst=5

[Service]
User=prometheus
Group=prometheus
Type=simple
Restart=on-failure
RestartSec=5s
ExecStart=/usr/local/bin/prometheus \
  --config.file=/etc/prometheus/prometheus.yml \
  --storage.tsdb.path=/data \
  --web.console.templates=/etc/prometheus/consoles \
  --web.console.libraries=/etc/prometheus/console_libraries \
  --web.listen-address=0.0.0.0:9090 \
  --web.enable-lifecycle

[Install]
WantedBy=multi-user.target
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696602042927/d7a1a28b-cc48-42e7-beaa-2b54ceb8371b.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

To automatically start the Prometheus after reboot, run enable:-

```powershell
sudo systemctl enable prometheus
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696602157011/4394589c-6623-4727-900b-448d927147d5.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

Then just start the Prometheus:-

```powershell
sudo systemctl start prometheus
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696602199097/382f4f76-389c-4f0e-9b15-b7ba86cba92d.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

To check the status of Prometheus run the following command:-

```powershell
sudo systemctl status prometheus
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696602276618/a938f20d-d254-4f97-9d92-7be9f483d934.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

Suppose you encounter any issues with Prometheus or are unable to start it. The easiest way to find the problem is to use the journalctl command and search for errors:-

```powershell
journalctl -u prometheus -f --no-pager
```

Now we can try to access it via the browser. I’m going to be using the IP address of the Ubuntu server. You need to open up on port 9090 to the public IP address.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1713508122404/d0705740-b191-4de9-b9c2-197ec1d85b10.jpeg?auto=compress,format&format=webp align="left")

If you go to targets, you should see only one – Prometheus target. It scrapes itself every 15 seconds by default.

### 3B:- Install Node Exporter on Ubuntu 22.04

Use the wget command to download the binary:-

```powershell
wget https://github.com/prometheus/node_exporter/releases/download/v1.6.1/node_exporter-1.6.1.linux-amd64.tar.gz
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696609307743/f37099e9-85be-4a71-a3a7-4a35b3d0bc8f.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

Extract the node exporter from the archive:-

```powershell
tar -xvf node_exporter-1.6.1.linux-amd64.tar.gz
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696609287909/7b7001b3-5161-4a49-846e-a7efd7ffc247.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

Move binary to the /usr/local/bin.

```powershell
sudo mv \
  node_exporter-1.6.1.linux-amd64/node_exporter \
  /usr/local/bin/
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696609266385/26a24b60-d5c6-4f28-a24c-16e4a22bc547.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

Verify that you can run the binary i.e. Node Exporter:-

```powershell
node_exporter --version
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696609222783/20664fa6-4d17-48c4-9d36-b10de1f390f1.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

Node Exporter has a lot of plugins that we can enable. If you run Node Exporter help you will get all the options:-

```powershell
node_exporter --help
```

collector.logind We’re going to enable the login controller, just for the demo.

Next, create a similar systemd unit file:-

```powershell
sudo vim /etc/systemd/system/node_exporter.service
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696609202473/282480ec-7a09-4472-9370-32c16b738593.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

**<mark>node_exporter.service</mark>**

```powershell
[Unit]
Description=Node Exporter
Wants=network-online.target
After=network-online.target
StartLimitIntervalSec=500
StartLimitBurst=5

[Service]
User=node_exporter
Group=node_exporter
Type=simple
Restart=on-failure
RestartSec=5s
ExecStart=/usr/local/bin/node_exporter \
    --collector.logind

[Install]
WantedBy=multi-user.target
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696609165286/5264f204-d2f4-4f24-a88f-bb3e871fc863.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

Replace Prometheus user and group to node\_exporter, and update the ExecStart command.

To automatically start the Node Exporter after reboot, enable the service:-

```powershell
sudo systemctl enable node_exporter
```

Then start the Node Exporter:-

```powershell
sudo systemctl start node_exporter
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696609144916/42cb02da-e3b8-4bfb-98db-bd40e20daed1.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

Check the status of Node Exporter with the following command:-

```powershell
sudo systemctl status node_exporter
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696609123201/01cf97f2-f66b-46ff-b513-3838699b7d9d.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

If you have any issues, check logs with journalctl:-

```powershell
journalctl -u node_exporter -f --no-pager
```

At this point, we have only a single target in our Prometheus. There are many different service discovery mechanisms built into Prometheus. For example, Prometheus can dynamically discover targets in AWS, GCP, and other clouds based on the labels. In the following tutorials, I’ll give you a few examples of deploying Prometheus in a cloud-specific environment. For this tutorial, let’s keep it simple and keep adding static targets. Also, I have a lesson on how to deploy and manage Prometheus in the Kubernetes cluster.

To create a static target, you need to add job\_name with static\_configs:-

```powershell
sudo vi /etc/prometheus/prometheus.yml
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696609098582/77721df5-85fc-478b-9b92-84fd32ea7056.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

**<mark>prometheus.yml</mark>**

```powershell
- job_name: node_export
    static_configs:
      - targets: ["localhost:9100"]
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696609076020/4394a954-0bb2-4b6f-9298-836803875641.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

By default, Node Exporter will be exposed on port 9100.

Since we enabled lifecycle management via API calls, we can reload the Prometheus config without restarting the service and causing downtime.

Before, restarting check if the config is valid:-

```powershell
promtool check config /etc/prometheus/prometheus.yml
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696609055992/898e9635-0b41-4d99-84b5-5855e12d6494.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

Then, you can use a POST request to reload the config:-

```powershell
curl -X POST http://localhost:9090/-/reload
```

Check the targets section

```powershell
http://<public_ip>:9090/targets
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1713508899107/53999536-0d4f-4aee-92f2-18c2e0869faf.jpeg?auto=compress,format&format=webp align="left")

### 3C:- Install Grafana on Ubuntu 22.04

To visualize metrics we can use Grafana. There are many different data sources that Grafana supports, one of them is Prometheus.

First, let’s make sure that all the dependencies are installed.

```powershell
sudo apt-get install -y apt-transport-https software-properties-common
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696608978738/0309b7a3-ef29-432a-8983-0aea3b18f7a1.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

Next, add the GPG key:-

```powershell
wget -q -O - https://packages.grafana.com/gpg.key | sudo apt-key add -
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696608959191/32dc0008-45e8-4988-850e-fdc98f2d5f44.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

Add this repository for stable releases:-

```powershell
echo "deb https://packages.grafana.com/oss/deb stable main" | sudo tee -a /etc/apt/sources.list.d/grafana.list
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696608939223/2dab0c38-72fe-4889-925d-5840fb32ee50.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

After you add the repository, update and install Garafana:-

```powershell
sudo apt-get update
sudo apt-get -y install grafana
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696608905039/8837f209-509e-4baa-b271-3e9d017b7b0e.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

To automatically start the Grafana after reboot, enable the service:-

```powershell
sudo systemctl enable grafana-server
sudo systemctl start grafana-server
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696608856213/e5be057d-3925-470c-9f04-5e3c894c6784.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

To check the status of Grafana, run the following command:-

```powershell
sudo systemctl status grafana-server
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696608831214/fcc119b0-b615-489c-b860-4aa29a85c3fb.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

Go to `http://<public_ip>:3000` and log in to the Grafana using default credentials. The username is admin, and the password is admin as well.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1713526977106/13831a20-5b52-4393-8526-59e34e8c6369.jpeg?auto=compress,format&format=webp align="left")

When you log in for the first time, you get the option to change the password.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1713526942100/c9762213-84f4-4052-b551-28012007d52a.jpeg?auto=compress,format&format=webp align="left")

To visualize metrics, you need to add a data source first:-

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1713527078377/86b34c08-38d9-4708-9eea-99b514377e69.jpeg?auto=compress,format&format=webp align="left")

Click Add data source and select Prometheus:-

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1713527117437/25142426-caf5-4c9e-b8bb-0e261f95ab57.jpeg?auto=compress,format&format=webp align="left")

For the URL, enter [**localhost:9090**](http://localhost:9090/) and click Save and test. You can see Data source is working or not:-

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1713527185842/17f91136-7cdd-4ecd-a21a-7cba7990c43d.jpeg?auto=compress,format&format=webp align="left")

Click on Save and Test:-

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1713527264642/59b01a71-8bab-40f0-9bbf-74368bb12dab.jpeg?auto=compress,format&format=webp align="left")

Let’s add Dashboard for a better view:-

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1713527358947/47c38d14-081e-4aa0-912d-8ec8e34e88a5.jpeg?auto=compress,format&format=webp align="left")

Click on Import Dashboard paste this code <mark>1860</mark> and click on load:-

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1713527423870/dad4a264-d81d-48ae-ab81-1a540e69e4f1.jpeg?auto=compress,format&format=webp align="left")

Select the Data Source and click on Import:-

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1713527506683/3fedab08-c4a6-4db8-81dd-c5e9ec629c9e.jpeg?auto=compress,format&format=webp align="left")

You will see this output like this:-

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1713527562015/34741b4d-3db1-4dde-bc93-d7ad898959e0.jpeg?auto=compress,format&format=webp align="left")

# **Step 4:- Install the Prometheus Plugin and Integrate it with the Prometheus server**

Let’s Monitor <mark>JENKINS SYSTEM NOW</mark>

Go to Manage Jenkins –&gt; Plugins –&gt; Available Plugins

Search for `Prometheus and install it`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1713527812141/0c590e6f-d396-4e2e-bee8-8a92089890a6.jpeg?auto=compress,format&format=webp align="left")

Once that is done you will Prometheus is set to `/Prometheus` path in system configurations:-

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696611956419/c83ac5ca-c7b6-45bf-9daa-149a6e96f784.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

Nothing to change click on apply and save

To create a static target, you need to add job\_name with static\_configs, go to Prometheus server:-

```powershell
sudo vim /etc/prometheus/prometheus.yml
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696612013869/ea167d82-1787-44d4-87e8-edfaf982ad36.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

Paste below code:-

```powershell
- job_name: 'jenkins'
    metrics_path: '/prometheus'
    static_configs:
      - targets: ['<jenkins-ip>:8080']
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696612070770/6c7bdfc2-6d68-4149-889e-2bd1bfbb0ae3.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

Before, restarting check if the config is valid or not:-

```powershell
promtool check config /etc/prometheus/prometheus.yml
```

Then, you can use a POST request to reload the config:-

```powershell
curl -X POST http://localhost:9090/-/reload
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696612139980/7c9d3a0f-5e12-4009-9943-24886da93bf2.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

Now again check the targets section:-

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1713528069980/43ac04b1-a130-4b70-a888-d659295580a2.jpeg?auto=compress,format&format=webp align="left")

Let’s add Dashboard for a better view in Grafana

Click On Dashboard –&gt; + symbol –&gt; Import Dashboard

Use Id `9964` and click on load

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1713528128557/28a3a414-6cc8-4356-b26b-7ed09f93ac42.jpeg?auto=compress,format&format=webp align="left")

Select the data source and click on Import:-

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1713528191254/b4805c17-af0f-4a01-8a4c-8ef4ccd6ce9a.jpeg?auto=compress,format&format=webp align="left")

Now you will see the Detailed overview of Jenkins:-

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1713528245829/07af8de8-cd31-401c-8185-447c26e072a9.jpeg?auto=compress,format&format=webp align="left")

---

# Step 5:- Email Integration With Jenkins and Plugin setup

Install `Email Extension Plugin` in Jenkins

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694164210365/4c78af7c-80a6-4442-b9cc-ee87b6956c1a.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

Go to your Gmail and click on your profile

Then click on Manage Your Google Account –&gt; click on the security tab on the left side panel you will get this page(provide mail password):-

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694164383650/5f0522cd-a90d-4f8c-8490-bfbae7f2191f.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

2-step verification should be enabled.

Search for the app in the search bar you will get app passwords like the below image:-

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694164475761/1c3e3229-acfd-4e97-825d-4bd8d8b316bb.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694164556725/f8a7bcdc-c65e-4c18-b6a2-d9d388594b9e.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

Click on other and provide your name and click on Generate and copy the password:-

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696838555126/14ef8a94-c402-4538-ac96-5057adb09edf.png?auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

Once the plugin is installed in Jenkins, click on manage Jenkins –&gt; configure system there under the E-mail Notification section configure the details as shown in the below image:-

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1713528550926/aab47d71-a6ce-4128-b53e-67cc117c59ea.jpeg?auto=compress,format&format=webp align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1713528638459/cf71a4ae-a5ff-45f5-8f28-7dca97322f53.jpeg?auto=compress,format&format=webp align="left")

Click on Apply and save.

Click on Manage Jenkins–&gt; credentials and add your mail username and generated password:-

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1713528784361/433c8902-77fb-444c-803e-8facc70b28e2.jpeg?auto=compress,format&format=webp align="left")

This is to just verify the mail configuration

Now under the Extended E-mail Notification section configure the details as shown in the below images:-

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1713528860200/98a36168-6c17-4b42-b345-f5d9b691b5e0.jpeg?auto=compress,format&format=webp align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694164940903/25104e50-fb02-4e8b-8c0d-f0c02f486975.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694164952910/0b6f0b17-238d-4d5d-ba57-dfe6818e8f09.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

Click on Apply and save.

```powershell
post {
     always {
        emailext attachLog: true,
            subject: "'${currentBuild.result}'",
            body: "Project: ${env.JOB_NAME}<br/>" +
                "Build Number: ${env.BUILD_NUMBER}<br/>" +
                "URL: ${env.BUILD_URL}<br/>",
            to: 'postbox.aj99@gmail.com',  #change Your mail
            attachmentsPattern: 'trivyfs.txt,trivyimage.txt'
        }
    }
```

Next, we will go in to Jenkins and start to configure our Pipeline in Jenkins.

---

---

## **Step 6:- Install Plugins like JDK, Sonarqube Scanner, NodeJs, OWASP Dependency Check**

### 6A:- Install Plugins

Goto Manage Jenkins →Plugins → Available Plugins →

Install below plugins

1 → Eclipse Temurin Installer (Install without restart)

2 → SonarQube Scanner (Install without restart)

3 → NodeJs Plugin (Install Without restart)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694160106164/d829e70f-9a23-4d03-a427-887d779aa141.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695227031117/e7a88b82-e007-465f-8c7f-b911c0e5f658.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

### 6B:- Configure Java and Nodejs in Global Tool Configuration

Goto Manage Jenkins → Tools → Install JDK(17) and NodeJs(16)→ Click on Apply and Save

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694160282666/7565037d-cf4f-4034-b55a-7028e580e3f8.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695403120569/3010e514-d64c-438a-85eb-d340ed5d3331.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

### 6C:- Create a Job

Create a job and give the name of your choice, select pipeline and click on OK.

---

# Step 7:- Create a Pipeline Project in Jenkins using a Declarative Pipeline

Grab the Public IP Address of your EC2 Instance, Sonarqube works on Port 9000, so &lt;Public IP&gt;:9000. Goto your Sonarqube Server. Click on Administration → Security → Users → Click on Tokens and Update Token → Give it a name → and click on Generate Token

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694160792404/611ddf2a-9c2c-414a-ad3a-2ba84f8942ca.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

click on update Token:-

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694160866134/49f34dd2-de41-455c-aee0-f1ffe13d8488.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

Create a token with a name and generate:-

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694160967625/a96320b2-3eda-411e-bb44-20092b8a79ec.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

Copy Token.

Then, go to Jenkins Dashboard → Manage Jenkins → Credentials → Add Secret Text. It should look like this:-

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694161147409/35b423f8-e7e4-402e-895b-cd1869b8a170.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

You will this page once you click on create:-

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694161221410/9a7a6f3f-fd40-4bbb-8857-bf2ffb8e6895.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

Now, go to Dashboard → Manage Jenkins → System and Add like the below image:-

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694161318710/738bd6ea-c374-4c76-9234-5ec09cfe754f.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

Click on Apply and Save

The Configure System option is used in Jenkins to configure different server

Global Tool Configuration is used to configure different tools that we install using Plugins

We will install a sonar scanner in the tools.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694161414550/efa6ef74-29e5-41c4-a81e-e6c528048c9f.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

In the Sonarqube Dashboard add a quality gate also

Administration–&gt; Configuration–&gt;Webhooks

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1713529456300/95005a27-32c3-4a9f-87fa-9f32e47b5a1e.jpeg?auto=compress,format&format=webp align="left")

Click on Create:-

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694242794858/85015d2b-1c59-435a-b058-1db98f215b18.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

Now,

```powershell
#in url section of quality gate
<http://jenkins-public-ip:8080>/sonarqube-webhook/
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1713529545629/58a18708-31fb-4191-b616-b2b9de4f6244.jpeg?auto=compress,format&format=webp align="left")

Let’s go to our Pipeline and add the script in our Pipeline Script:-

```powershell
pipeline{
    agent any
    tools{
        jdk 'jdk17'
        nodejs 'node16'
    }
    environment {
        SCANNER_HOME=tool 'sonar-scanner'
    }
    stages {
        stage('clean workspace'){
            steps{
                cleanWs()
            }
        }
        stage('Checkout from Git'){
            steps{
                git branch: 'main', url: 'your_github_URL_here'
            }
        }
        stage("Sonarqube Analysis "){
            steps{
                withSonarQubeEnv('sonar-server') {
                    sh ''' $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=Application \
                    -Dsonar.projectKey=Application ''' # you can change the name and key here 
                }
            }
        }
        stage("quality gate"){
           steps {
                script {
                    waitForQualityGate abortPipeline: false, credentialsId: 'Sonar-token'
                }
            }
        }
        stage('Install Dependencies') {
            steps {
                sh "npm install"
            }
        }
    }
    post {
     always {
        emailext attachLog: true,
            subject: "'${currentBuild.result}'",
            body: "Project: ${env.JOB_NAME}<br/>" +
                "Build Number: ${env.BUILD_NUMBER}<br/>" +
                "URL: ${env.BUILD_URL}<br/>",
            to: 'your_mail_id@gmail.com',
            attachmentsPattern: 'trivyfs.txt,trivyimage.txt'
        }
    }
}
```

Click on Build now, you will see the stage view like this:-

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695231229497/f9d97aa9-90ba-49cf-b082-9df24ee86c4b.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

To see the report, you can go to SonarQube Server and go to Projects:- (You will get the view of the SonarQube Report of your project like this)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1713529818305/f6fbfebd-9d4e-4ab3-bce5-615268ece5ca.jpeg?auto=compress,format&format=webp align="left")

You can now see the report has been generated and the status shows as passed. Now, you can see that there are number of lines of code is scanned. To see a detailed report, you can go to issues.

---

# **Step 8:- Install OWASP Dependency Check Plugins**

Go to Dashboard → Manage Jenkins → Plugins → OWASP Dependency-Check. Click on it and install it without restart.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694162570631/a0da6454-e85a-4e27-908a-255b024bf834.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

First, we configured the Plugin and next, we had to configure the Tool

Go to Dashboard → Manage Jenkins → Tools →

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694162653334/158f6b94-7c92-4556-9151-6213a003b431.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

Click on Apply and Save here.

Now go configure → Pipeline and add this stage to your pipeline and build:-

```powershell
stage('OWASP FS SCAN') {
            steps {
                dependencyCheck additionalArguments: '--scan ./ --disableYarnAudit --disableNodeAudit', odcInstallation: 'DP-Check'
                dependencyCheckPublisher pattern: '**/dependency-check-report.xml'
            }
        }
        stage('TRIVY FS SCAN') {
            steps {
                sh "trivy fs . > trivyfs.txt"
            }
        }
```

The stage view would look like this,

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695231335082/b5330f0d-67a5-43df-866d-c41d64627f9f.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

You will see that in status, a graph will also be generated and Vulnerabilities. (There might be a possibility that you will get the message of "No Vulnerabilities Found" but that is completely alright)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695231385639/64d49427-ce7b-4723-a432-faf02dbca838.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

---

# **Step 9:- Installing Docker Scout, Docker Image Build and Push**

Before Adding pipeline install Docker Scout:

```powershell
docker login    #use credentials to login
curl -sSfL https://raw.githubusercontent.com/docker/scout-cli/main/install.sh | sh -s -- -b /usr/local/bin
```

We need to install the Docker tool in our system, Goto Dashboard → Manage Plugins → Available plugins → Search for Docker and install these plugins:-

`Docker`

`Docker Commons`

`Docker Pipeline`

`Docker API`

`docker-build-step`

and click on install without restart

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694162971794/4e289fe1-c3b9-48d0-8efd-2b8b47118e71.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

Now, goto Dashboard → Manage Jenkins → Tools →

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694163030620/59df4527-29d4-41df-8dcd-501e04fda7eb.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

Add Docker Hub Username and Password under Global Credentials:- (you will be adding your Docker Hub username in the "USERNAME" section below)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1713530516956/63943485-9dfc-4d0f-b006-1382d34cbe13.jpeg?auto=compress,format&format=webp align="left")

Add this stage to Pipeline Script:-

```powershell
stage('Docker Scout FS') {
            steps {
                script{
                   withDockerRegistry(credentialsId: 'docker', toolName: 'docker'){
                       sh 'docker-scout quickview fs://.'
                       sh 'docker-scout cves fs://.'
                   }
                }   
            }
        }
stage("Docker Build & Push"){
            steps{
                script{
                   withDockerRegistry(credentialsId: 'docker', toolName: 'docker'){
                       sh "docker build -t hotstar ."
                       sh "docker tag netflix yash5090/hotstar:latest "
                       sh "docker push yash5090/hotstar:latest "
                    }
                }
            }
        }
        stage("TRIVY"){
            steps{
                sh "trivy image yash5090/hotstar:latest > trivyimage.txt"
            }
        }
stage('Docker Scout Image') {
            steps {
                script{
                   withDockerRegistry(credentialsId: 'docker', toolName: 'docker'){
                       sh 'docker-scout quickview yash5090/hotstar:latest'
                       sh 'docker-scout cves yash5090/hotstar:latest'
                       sh 'docker-scout recommendations yash5090/hotstar:latest'
                   }
                }   
            }
        }
```

You will see the output below, with a dependency trend:-

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695231457022/078e9995-b27f-47fd-9add-bffe2426107b.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

When you log in to Docker Hub, you will see a new image is created.

---

# **Step 10:- Deploy the image using Docker**

Now Run the container to see if it is coming up or not by adding the below stage:-

```powershell
stage('Deploy to container'){
            steps{
                sh 'docker run -d --name netflix -p 8081:80 yash5090/hotstar:latest'
            }
        }
```

Stage View will be like this:-

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695231634338/483ee533-5144-4424-b55f-a74ebc38769f.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

On getting the above successful Output, use your `<Jenkins-public-ip:8081>`

And, you will get this output:-

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704297859314/8c8bf02e-805a-48f1-9de8-36b5b39f894f.png?auto=compress,format&format=webp align="left")

---

# **Step 11:- Kubernetes Master and Slave server setup on Ubuntu (20.04)**

Take-Two Ubuntu 20.04 instances one for k8s master and the other one for worker.

Install Kubectl on Jenkins machine also.

**<mark>Kubectl is to be installed on Jenkins also</mark>**

```powershell
sudo apt update
sudo apt install curl
curl -LO https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
kubectl version --client
```

### Part 1:- Master Node

```powershell
sudo hostnamectl set-hostname K8s-Master
```

### Worker Node

```powershell
sudo hostnamectl set-hostname K8s-Worker
```

### Part 2:- Both Master & Worker Node

```powershell
sudo apt-get update
sudo apt-get install -y docker.io
sudo usermod –aG docker Ubuntu
newgrp docker
sudo chmod 777 /var/run/docker.sock
```

```powershell
sudo apt-get update
```

```powershell
sudo apt-get install -y apt-transport-https ca-certificates curl gpg
```

```powershell
curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.29/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
```

```powershell
echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.29/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list
```

```powershell
sudo apt-get update
sudo apt-get install -y kubelet kubeadm kubectl
sudo apt-mark hold kubelet kubeadm kubectl
```

### Part 3:- k8s Master

```powershell
sudo kubeadm init --pod-network-cidr=10.244.0.0/16
# in case your in root exit from it and run below commands
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml
```

### ———-Worker Node————

```powershell
sudo kubeadm join <master-node-ip>:<master-node-port> --token <token> --discovery-token-ca-cert-hash <hash>
```

Copy the config file to Jenkins master or the local file manager and save it:-

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694164048426/b0b0152d-aca6-474f-8d88-a9c28dd9d703.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

copy it and save it in documents or another folder save it as secret-file.txt

Note: create a secret-file.txt in your file explorer save the config in it and use this at the Kubernetes credential section.

Install Kubernetes Plugin, Once it’s installed successfully:-

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694163896514/5edda1d6-b9a3-45c2-9bcf-e677939191cf.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

goto manage Jenkins –&gt; manage credentials –&gt; Click on Jenkins global –&gt; add credentials

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694163948237/0e01b94e-c1e4-4fd2-8f5d-730df240a5b5.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

### Now, Install Node\_exporter on both master and worker servers

Let’s add Node\_exporter on Master and Worker to monitor the metrics

First, let’s create a system user for Node Exporter by running the following command:-

```powershell
sudo useradd \
    --system \
    --no-create-home \
    --shell /bin/false node_exporter
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696609331597/ab4ca15e-fb04-4294-a439-72fbfb84c178.png?auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

Use the wget command to download the binary:-

```powershell
wget https://github.com/prometheus/node_exporter/releases/download/v1.6.1/node_exporter-1.6.1.linux-amd64.tar.gz
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696609307743/f37099e9-85be-4a71-a3a7-4a35b3d0bc8f.png?auto=compress,format&format=webp align="left")

Extract the node exporter from the archive:-

```powershell
tar -xvf node_exporter-1.6.1.linux-amd64.tar.gz
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696609287909/7b7001b3-5161-4a49-846e-a7efd7ffc247.png?auto=compress,format&format=webp align="left")

Move binary to the /usr/local/bin:-

```powershell
sudo mv \
  node_exporter-1.6.1.linux-amd64/node_exporter \
  /usr/local/bin/
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696609266385/26a24b60-d5c6-4f28-a24c-16e4a22bc547.png?auto=compress,format&format=webp align="left")

Verify that you can run the binary:-

```powershell
node_exporter --version
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696609222783/20664fa6-4d17-48c4-9d36-b10de1f390f1.png?auto=compress,format&format=webp align="left")

Node Exporter has a lot of plugins that we can enable. If you run Node Exporter help you will get all the options:-

```powershell
node_exporter --help
```

–collector.logind We’re going to enable the login controller, just for the demo.

Next, create a similar systemd unit file:-

```powershell
sudo vi /etc/systemd/system/node_exporter.service
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696609202473/282480ec-7a09-4472-9370-32c16b738593.png?auto=compress,format&format=webp align="left")

**<mark>node_exporter.service</mark>**

```powershell
[Unit]
Description=Node Exporter
Wants=network-online.target
After=network-online.target
StartLimitIntervalSec=500
StartLimitBurst=5

[Service]
User=node_exporter
Group=node_exporter
Type=simple
Restart=on-failure
RestartSec=5s
ExecStart=/usr/local/bin/node_exporter \
    --collector.logind

[Install]
WantedBy=multi-user.target
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696609165286/5264f204-d2f4-4f24-a88f-bb3e871fc863.png?auto=compress,format&format=webp align="left")

Replace Prometheus user and group to node\_exporter, and update the ExecStart command.

To automatically start the Node Exporter after reboot, enable the service:-

```powershell
sudo systemctl enable node_exporter
```

Then start the Node Exporter:-

```powershell
sudo systemctl start node_exporter
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696609144916/42cb02da-e3b8-4bfb-98db-bd40e20daed1.png?auto=compress,format&format=webp align="left")

Check the status of Node Exporter with the following command:-

```powershell
sudo systemctl status node_exporter
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696609123201/01cf97f2-f66b-46ff-b513-3838699b7d9d.png?auto=compress,format&format=webp align="left")

If you have any issues, check logs with journalctl :-

```powershell
journalctl -u node_exporter -f --no-pager
```

At this point, we have only a single target in our Prometheus. There are many different service discovery mechanisms built into Prometheus. For example, Prometheus can dynamically discover targets in AWS, GCP, and other clouds based on the labels. In the following tutorials, I’ll give you a few examples of deploying Prometheus in a cloud-specific environment. For this tutorial, let’s keep it simple and keep adding static targets. Also, I have a lesson on how to deploy and manage Prometheus in the Kubernetes cluster.

To create a static target, you need to add job\_name with static\_configs. Go to Prometheus server:-

```powershell
sudo vi /etc/prometheus/prometheus.yml
```

**<mark>prometheus.yml</mark>**

```powershell
- job_name: node_export_masterk8s
    static_configs:
      - targets: ["<master-ip>:9100"]
  - job_name: node_export_workerk8s
    static_configs:
      - targets: ["<worker-ip>:9100"]
```

By default, Node Exporter will be exposed on port 9100:-

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696838151827/7e21e323-e1fb-48ae-bcb2-67d79ddafa25.png?auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

Since we enabled lifecycle management via API calls, we can reload the Prometheus config without restarting the service and causing downtime.

Before, restarting check if the config is valid or not:-

```powershell
promtool check config /etc/prometheus/prometheus.yml
```

Then, you can use a POST request to reload the config:-

```powershell
curl -X POST http://localhost:9090/-/reload
```

Check the targets section:-

```powershell
http://<public_ip>:9090/targets
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696838181332/62b6e4b5-3cf3-472b-ad73-c305822b6846.png?auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

final step to deploy on the Kubernetes Cluster:-

```powershell
stage('Deploy to kubernets'){
            steps{
                script{
                    dir('Kubernetes') {
                        withKubeConfig(caCertificate: '', clusterName: '', contextName: '', credentialsId: 'k8s', namespace: '', restrictKubeConfigAccess: false, serverUrl: '') {
                                sh 'kubectl apply -f deployment.yml'
                                sh 'kubectl apply -f service.yml'
                        }
                    }
                }
            }
        }
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695231979645/41227fb6-e1da-4f60-a120-00d424d73fb9.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

In the Kubernetes cluster(Master Server) give this command:-

```powershell
kubectl get all
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694165240130/0cec6712-24b4-4715-8143-2083a367016e.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

---

# Step 12:- Terminate the AWS EC2 Instances.

---

# **<mark>Full steps of CI/CD Pipeline</mark> <mark>Below👇</mark>**

---

# ***CI/CD Pipeline:-***

```powershell
pipeline{
    agent any
    tools{
        jdk 'jdk17'
        nodejs 'node16'
    }
    environment {
        SCANNER_HOME=tool 'sonar-scanner'
    }
    stages {
        stage('clean workspace'){
            steps{
                cleanWs()
            }
        }
        stage('Checkout from Git'){
            steps{
                git branch: 'main', url: 'your_github_URL_here'
            }
        }
        stage("Sonarqube Analysis "){
            steps{
                withSonarQubeEnv('sonar-server') {
                    sh ''' $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=Application \
                    -Dsonar.projectKey=Application '''  # you can change the name and key here as per ypur choice
                }
            }
        }
        stage("quality gate"){
           steps {
                script {
                    waitForQualityGate abortPipeline: false, credentialsId: 'Sonar-token'
                }
            }
        }
        stage('Install Dependencies') {
            steps {
                sh "npm install"
            }
        }
        stage('OWASP FS SCAN') {
            steps {
                dependencyCheck additionalArguments: '--scan ./ --disableYarnAudit --disableNodeAudit', odcInstallation: 'DP-Check'
                dependencyCheckPublisher pattern: '**/dependency-check-report.xml'
            }
        }
        stage('TRIVY FS SCAN') {
            steps {
                sh "trivy fs . > trivyfs.txt"
            }
        }
        stage('Docker Scout FS') {
            steps {
                script{
                   withDockerRegistry(credentialsId: 'docker', toolName: 'docker'){
                       sh 'docker-scout quickview fs://.'
                       sh 'docker-scout cves fs://.'
                   }
                }   
            }
        }
        stage("Docker Build & Push"){
            steps{
                script{
                   withDockerRegistry(credentialsId: 'docker', toolName: 'docker'){
                       sh "docker build -t hotstar ."
                       sh "docker tag netflix yash5090/hotstar:latest "
                       sh "docker push yash5090/hotstar:latest "
                    }
                }
            }
        }
        stage("TRIVY"){
            steps{
                sh "trivy image yash5090/hotstar:latest > trivyimage.txt"
            }
        }
        stage('Docker Scout Image') {
            steps {
                script{
                   withDockerRegistry(credentialsId: 'docker', toolName: 'docker'){
                       sh 'docker-scout quickview yash5090/hotstar:latest'
                       sh 'docker-scout cves yash5090/hotstar:latest'
                       sh 'docker-scout recommendations yash5090/hotstar:latest'
                   }
                }   
            }
        }
        stage('Deploy to container'){
            steps{
                sh 'docker run -d --name netflix -p 8081:80 yash5090/hotstar:latest'
            }
        }
        stage('Deploy to kubernets'){
            steps{
                script{
                    dir('Kubernetes') {
                        withKubeConfig(caCertificate: '', clusterName: '', contextName: '', credentialsId: 'k8s', namespace: '', restrictKubeConfigAccess: false, serverUrl: '') {
                                sh 'kubectl apply -f deployment.yml'
                                sh 'kubectl apply -f service.yml'
                        }
                    }
                }
            }
        }
    }
    post {
     always {
        emailext attachLog: true,
            subject: "'${currentBuild.result}'",
            body: "Project: ${env.JOB_NAME}<br/>" +
                "Build Number: ${env.BUILD_NUMBER}<br/>" +
                "URL: ${env.BUILD_URL}<br/>",
            to: 'your_mail_id@gmail.com',
            attachmentsPattern: 'trivyfs.txt,trivyimage.txt'
        }
    }
}
```