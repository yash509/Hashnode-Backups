---
title: "Untwist the world of Docker - P1"
datePublished: Sun Mar 24 2024 07:45:14 GMT+0000 (Coordinated Universal Time)
cuid: clu57s3ab00000al31x7fccyb
slug: untwist-the-world-of-docker-p1
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1711266219399/c7b50df4-12cd-42dc-9dcf-d057dd7b35a7.avif
tags: cloud, docker, aws, azure, devops, containerization, gcp, devsecops, 2articles1week

---

# What is Docker?

Docker is a containerization platform that enables developers to package, deploy, and run applications with their dependencies. Basically, the docker is a Linux-based, open-source containerization platform that developers use to build, run, and package the applications for deployment using docker containers. The containerization of applications has become increasingly more popular due to its efficiency, consistency, and portability across different environments and systems. The docker uses containerization technology, which allows applications to be bundled into lightweight, standalone units called containers. These docker containers contains everything that is needed to run the applications, including application's source code, runtime, system tools, libraries, and various other settings.

Like we all know that the concept of hosting the applications on virtual machines is old, slow and much time taking as compared to the new era of Containerization of applications using docker containers because the containers share the host system's kernel, making them more lightweight and faster to start up the applications.

One of major key component of Docker is the Docker Engine, which provides an great environment for creating and managing docker containers. The Developers or DevOps Engineers use Docker Engine's CLI or API to build docker container images by using the Dockerfiles, which are text files containing instructions for assembling the application's environment. These images can then be stored in docker registries, such as Docker Hub, for easy distribution and sharing of applications in the form of docker images.

Moreover, the docker facilitates the collaboration and DevOps practices. Teams can use Docker to create consistent development, testing, and production environments, by enhancing team collaboration and accelerating the software delivery pipeline. In addition to all these stuffs, the docker integrates with the popular DevOps tools for automated testing, continuous integration (CI), and continuous deployment (CD), which enables the organizations to streamline or enhance their workflows and deliver software more faster, efficiently and effectively.

Overall the, docker revolutionizes the way for developers to build, ship, and run the applications by providing a standardized, efficient, and portable containerization platform. Its benefits include consistency, scalability, maximum resource utilization, dependency management, portability, and support for the modern DevOps practices. As containerization continues to reshape the software development landscape, Docker remains a leading solution for container orchestration and deployment processes.

For example:- The docker can containerize the database of an application. With such a framework, you can scale or maintain the database independently from other modules or components of the application without impacting the workloads of other critical systems.

The Docker or the platforms of containers launched in 2013 by Docker Inc.

# Benefits of using Docker?

Some benefits of using Docker are as follows:

1. DevOps Facilitation: Docker integrates seamlessly with DevOps practices, enabling automation, collaboration, and continuous integration/continuous deployment (CI/CD) workflows, which accelerate software delivery.
    
2. Utilization of Resources: Docker optimizes resources utilization by allowing applications to share the host system's kernel, resulting in lower overhead and better performance as compared to the traditional virtualization process.
    
3. High Speed: Docker containers start up and shut down quickly, which enables the faster development cycles and deployment processes as compared to traditional virtual machines.
    
4. Consistency: Docker ensures that applications run consistently across different environments, reducing the "it works on my machine" problem commonly encountered in software development process.
    
5. Isolation: Docker containers provide isolation for the applications and their dependencies, by enhancing security and by minimizing the impact of any potential vulnerabilities.
    
6. **Larger Community and Larger Ecosystem**: Docker has a large and active community, along with an extensive ecosystem of tools, libraries, and pre-built images available on Docker Hub, which streamlines the development and deployment tasks.
    
7. High Scalability: Docker facilitates rapid scaling of applications by allowing containers to be quickly shut up or down in response to changing demand, ensuring optimal resources allocation.
    
8. Portability: The docker containers packaged with Docker include all the dependencies, making them easily portable across different environments, from development to production environments, without any kind of compatibility issues.
    
9. Efficiency: Docker's lightweight containers enable efficient resources utilization, by allowing for more applications to be run on the same hardware as compared to the traditional virtual machines.
    
10. Dependency Management: The docker simplifies the dependency management by packaging dependencies within docker containers, reducing conflicts and ensuring reproducibility across various environments.
    

# How does the Docker Works?

Docker works by utilizing the containerization technology to package, deploy, and run applications in the isolated environments known as containers. The core component of Docker is the Docker Engine, which comprises of the several components that work together to manage the docker containers more efficiently and effectively.

The developers or the DevOps Engineers create the Docker containers using Dockerfiles, which are text files containing instructions for assembling an application's environment. These instructions specify the base image to use, along with the additional layers that configure the application's dependencies, libraries, and settings. Dockerfiles provide the standardized way to define the environment, by making it easier to deploy the applications across various different environments.

Once a Dockerfile is created, developers use the Docker Engine to build the container image. The Docker Engine reads the Dockerfile and executes the instructions, and builds up the application's environments. Once the container image is built, it can be stored in a docker registry, such as Docker Hub, for easy distribution and sharing of application. Docker Registries serve as repositories for storing container images, by allowing developers to pull images from the docker registry to their local environment and deploy them to remote servers. When the Docker Application Image is ready, the developers or the DevOps Engineers use the Docker Engine to create a docker container instance from the container image. The Docker Engine manages container lifecycle operations, such as starting, stopping, pausing, and restarting containers. Each docker container runs in isolation, with its own filesystem, network, and process space, but shares the host system's kernel, making containers lightweight and efficient in working and performance.

Containers can be easily created, modified, and destroyed without affecting other containers or the host system. This flexibility allows developers to experiment with different configurations, roll back changes, and scale applications as per needs. Docker also provides the various networking and storage solutions to connect containers and manage data. Docker's networking features enables communication between docker containers running on the same host or across the different hosts, by promoting the use of microservices architectures and distributed applications. Docker's storage options allow containers to keep data across container restarts and migrations, by ensuring higher data integrity and availability.

Moreover, the docker integrates with orchestration platforms, such as Docker Swarm and Kubernetes, to manage clusters of containers. Orchestration platforms automate container deployment, scaling, and load balancing, making it easier to manage complex containerized applications in production environments.

# Components of Docker?

Some key components of Docker are as follows:

1. Docker Engine: The Docker Engine handles container lifecycle operations, including building images, running containers, and managing container networks and storage.
    
2. Dockerfiles: The Dockerfiles provide a standardized way to define the application's dependencies and settings, making it easier to reproduce the environment across different environments. In other words, the Dockerfiles are the text files that contain instructions for building Docker images. These instructions specify the base image to use, along with additional layers that configure the application's environment.
    
3. Docker Registry: Docker registry are repositories for Docker images, where images can be stored, shared, and distributed. Docker Hub is the official public registry provided by Docker.
    
4. Docker Compose: Docker Compose is a tool for defining and managing multi-container Docker applications. The Docker Compose uses YAML files to specify the services, networks, and volumes that make up an application.
    
5. Docker CLI: The Docker command-line interface (CLI) is a tool used to interact with the Docker Engine and manage Docker resources. The Docker CLI provides commands for building images, running containers, etc.
    
6. Docker Swarm: The Docker Swarm is a Docker's native clustering and orchestration platform for managing clusters of hosts in Docker. The Docker Swarm enables users to deploy, scale, and manage containerized applications across multiple hosts or servers.
    
7. Networking in Docker: Docker provides networking solutions to enable communication between containers running on the same host or across different hosts.
    
8. Volumes in Docker : The docker volumes are persistent storage mechanisms that allow containers to store and access data beyond the docker container's lifecycle.
    
9. Docker Images: Docker images are the lightweight, standalone, executable packages that contains everything that is needed to run an application, including source code, runtime, libraries, and various other dependencies.
    
10. Docker Containers: The Docker Containers are like the instances of Docker images that are running in isolation on a host machine or host server.
    

# Docker Architecture Diagram

![Docker overview | Docker Docs](https://docs.docker.com/get-started/images/docker-architecture.webp align="left")

1. The Docker Client: The Docker client (`docker`) is the primary way that many Docker users interact with Docker.
    
2. The Docker Daemon: The Docker daemon (`dockerd`) listens for Docker API requests and manages Docker objects such as images, containers, networks, and volumes. Like for example, when you use commands such as `docker run`, the client sends these commands to `dockerd`, which carries out the task.
    
3. Docker Registry: Docker registry are repositories for Docker images, where images can be stored, shared, and distributed. Docker Hub is the official public registry provided by Docker.
    

# Benefits of using Docker in the Software Development Lifecycle (SDLC):-

Some benefits of using Docker in SDLC are as follows:

1. Building: The docker allows development teams to save time, effort, and money by *dockerizing* their applications into single or multiple modules.
    
2. Testing: With the help of docker, you can independently test each containerized application and the various components of application without impacting other components of the application.
    
3. Deploy & Maintain: The docker helps in reducing the fractions between teams by ensuring consistent versions of libraries and packages are used at every stage of the development process.
    

### Some popular tools along with which the Docker can use:

1. Kubernetes
    
2. Bit Bucket
    
3. MongoDB
    
4. Nginx
    
5. Redis, etc.
    

# Steps for Installing Docker Engine on Ubuntu

So, for Installing Docker on Ubuntu or on other similar distributions. Do follow these below steps:

```bash
$ sudo apt-get update
$ sudo apt-get install -y ca-certificates curl gnupg lsb-release
```

Now, for downloading and saving the GPG key that will be used to sign-in to the Docker repositories:

```bash
$ sudo mkdir -p /etc/apt/keyrings
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```

Now, for adding the repository to your package lists:

```bash
$ echo \ 
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

Now, update your package lists to include the new repository:

```bash
$ sudo apt-get update
```

Now, Finally, install the `docker-ce`, `docker-ce-cli`, and `containerd` packages:

```bash
$ sudo apt-get install -y docker-ce docker-ce-cli containerd.io
```

Now, let's discuss the use of the above mentioned packages:

* `docker-ce` – Is the Docker daemon that manages your containers.
    
* `docker-ce-cli` – Is the CLI you use to interact with the Docker daemon.
    
* `containerd.io` – The [containerd](https://containerd.io/) is a container runtime, it wrap ups the operating system features such as [cgroups](https://man7.org/linux/man-pages/man7/cgroups.7.html) to start and run your containers, based on the requests from the Docker daemon.
    

So, at last it's time to complete the whole installation by adding yourself to the docker group. This allows you to run docker CLI commands without using the `sudo` privileges. Commands for adding ourself to the docker group are:

```bash
$ sudo groupadd docker
$ sudo usermod -aG docker $USER
```

Now, for checking that whether the docker is working or not use The hello-world image on Docker Hub and this is how you can check it’s working by starting a basic hello-world container. Run the following command to start a container with the hello-world image:

```bash
$ docker run hello-world:latest
```

On running the above command you should see output like below:

```plaintext
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
2db29710123e: Pull complete 
Digest: sha256:c77be1d3a47d0caf71a82dd893ee61ce01f32fc758031a6ec4cf1389248bb833
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.
```

It then starts the container and shows its output to your terminal. All the lines from “Hello from Docker” onwards are emitted by the process inside the container. Now, you can say that now the docker installation is ready to use.

***In the next part we will be discussing about the Management of Security of Docker Containers.***