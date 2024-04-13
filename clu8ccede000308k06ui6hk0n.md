---
title: "Untwist the world of Docker - P3"
datePublished: Tue Mar 26 2024 12:16:19 GMT+0000 (Coordinated Universal Time)
cuid: clu8ccede000308k06ui6hk0n
slug: untwist-the-world-of-docker-p3
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1711451310944/b1f5cad6-dbaf-4073-8691-abdd02535514.avif
tags: cloud, blogging, docker, aws, azure, devops, gcp, devsecops, 2articles1week, devops-articles, docker-command

---

So, before moving ahead in this series of Docker and start discussing about the various examples of Dockerfiles, creating Docker Images using Dockerfiles and pushing it to Registry i.e. Docker Hub, Creating Docker Containers, etc.

Today, let's see the ultimate Docker Cheat sheet. A cheat sheet is a concise summary of important information that is meant to be used as a quick reference. In the context of Docker, a Docker cheat sheet is a summary of commonly used Docker commands and their options, as well as other useful information related to Docker. Cheat sheets can be helpful when learning a new tool or technology, as they provide a convenient way to quickly look up and remind ourself of key concepts and commands.

### <mark>LET'S BEGIN WITH DOCKER'S ULTIMATE CHEAT SHEET:</mark>

Command to view the Docker's Version:

```xml
docker --version
```

Command for logging in into the Docker Hub on the webserver like: Linux, Ubuntu, etc.:

```xml
docker login
```

Command for run a new container from an Docker Image:

```xml
docker run <Image Name>

// exmaple
docker run hello-world
```

Command for start a new container from an Docker Image and assigning it a name:

```xml
docker run --name CONTAINER_IMAGE

// exmaple
docker run --name web hello-world
```

Command for start a new container from an Docker Image and run container in background:

```xml
docker run -d <Image Name>

// exmaple
docker run -d hello-world
```

Command for start a new container from an Docker Image and run container in background and assign it a hostname:

```xml
docker run --hostname <HOSTNAME> <Image Name>

// exmaple
docker run --hostname steve hello-world
```

Command for start a new container from an Docker Image and map a Port to it:

```xml
docker run -p <HOSTPORT>:<CONTAINER PORT> <Image Name>

// exmaple
docker run -p 8080:80 hello-world
```

Command for start a new container from an Docker Image and map all the Port to it:

```xml
docker run -P <Image Name>

// exmaple
docker run -P hello-world
```

Command for start a new container from an Docker Image and run container in background and add a DNS entry:

```xml
docker run --add-host <HOSTNAME>:<Image IP>
```

Command for start a new container from an Docker Image but change the entry point:

```xml
docker run -it --entrypoint <EXECUTABLE IMAGE>

// exmaple
docker run -it --entrypoint bash hello-world
```

Command to view the list of a running Docker Container:

```xml
docker ps
```

Command to view the list of all running Docker Container:

```xml
docker ps -a
```

Command to stop a Docker Container:

```xml
docker stop <CONATINER NAME> or <CONATINER ID>

//example
docker stop sonarqube or e2g54umof0
```

Command to remove a Docker Container:

```xml
docker rm <CONATINER NAME> or <CONATINER ID>

//example
docker rm sonarqube or e2g54umof0
```

Command to remove a running Docker Container:

```xml
docker rm -f <CONATINER NAME> or <CONATINER ID>

//example
docker rm -f sonarqube or e2g54umof0
```

Command to start a stopped Docker Container:

```xml
docker start <CONATINER NAME> or <CONATINER ID>

//example
docker start sonarqube or e2g54umof0
```

Command to copy a file from a Docker Container to the Host:

```xml
docker cp <CONATINER NAME>:<SOURCE> <TARGET>

//example
docker start website:/index.html index.html
```

Command to copy a file from a Host to Docker Container:

```xml
docker cp <TARGET> <CONATINER NAME>:<SOURCE> 

//example
docker start index.html website:/index.html
```

Command to start a shell inside a running Docker Container:

```xml
docker run -it <CONATAINER> <EXECUTABLE NAME>

// exmaple
docker run -it website bash
```

Command to rename a Docker Container:

```xml
docker rename <OLD NAME> <NEW NAME>

// exmaple
docker run -it website king
```

Command to create an image out of Docker Container:

```xml
docker commit <CONTAINER NAME>

// exmaple
docker commit king
```

Command to download an Docker Image:

```xml
docker pull <IMAGE NAME>:<TAG>

// exmaple
docker pull nginx:latest
```

Command to push an Docker Image to Docker Hub:

```xml
docker push <IMAGE NAME>

// exmaple
docker push joker:1.0
```

Command to delete an Docker Image:

```xml
docker rmi <IMAGE NAME>

// exmaple
docker rmi joker
```

Command to view a list of all the Docker Images:

```xml
docker images
```

Command to remove all the dangling Docker Images:

```xml
docker image prune
```

Command for building a Docker Image using Dockerfile:

```xml
docker build <IMAGE NAME> .

//example
docker build netflix .
```

Command for Tagging a Docker Image:

```xml
docker tag <IMAGE NAME> <NEW IMAGE NAME>

//example
docker tag netflix netflix:19.0
```

Command for building a Docker Image using Dockerfile and Tagging it:

```xml
docker build -t <IMAGE DIRECTORY>

//example
docker build netflix:19.0 .
```

Command for saving a Docker Image to TAR file:

```xml
docker save <IMAGE> > <FILE NAME>

//example
docker save netflix > netflix.tar
```

Command for loading a Docker Image from a TAR file:

```xml
docker load -i <TAR FILE NAME>

//example
docker load -i netflix.tar
```

Command to view all logs of a Docker Container:

```xml
docker logs <CONTAINER NAME>

// exmaple
docker logs netflix
```

Command to view stats of running Docker Containers:

```xml
docker stats
```

Command to view processes of a running Docker Container:

```xml
docker top <CONTAINER NAME>

// exmaple
docker top netflix
```

Command to get detailed information of an object of Docker Image:

```xml
docker inspect <IMAGE NAME>

// exmaple
docker inspect netflix
```

Command to view all the modified files in a Docker Container:

```xml
docker diff <CONTAINER NAME>

// exmaple
docker diff netflix
```

Command to view all the mapped ports of a Docker Container:

```xml
docker port <CONTAINER NAME>

// exmaple
docker port netflix
```

So, this is the Ultimate Cheat Sheet for Docker which contains all the useful commands for Docker.

<mark>So finally, </mark> *<mark>In the next part we will be seeing the various examples of creating Dockerfiles, creating Docker Images and pushing it to Registry i.e. Docker Hub.</mark>*