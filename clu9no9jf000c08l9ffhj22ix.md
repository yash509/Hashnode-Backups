---
title: "Untwist the world of Docker - P4"
datePublished: Tue Mar 26 2024 18:30:00 GMT+0000 (Coordinated Universal Time)
cuid: clu9no9jf000c08l9ffhj22ix
slug: untwist-the-world-of-docker-p4
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1711534753772/568257fb-7d4a-4485-b6ab-e1a2da501334.avif
tags: cloud, blogging, docker, aws, azure, devops, containerization, gcp, devsecops, dockerfile, 2articles1week, docker-images, docker-hub

---

# What are Dockerfiles?

The Dockerfiles provide a standardized way to define the application's dependencies and settings, making it easier to reproduce the environment across different environments. In other words, the Dockerfiles are the text files that contain instructions for building Docker images. These instructions specify the base image to use, along with additional layers that configure the application's environment. Basically, the dockerfiles are text files used to define the configuration of a Docker image. Docker is a platform that allows developers to package their applications and dependencies into containers, which are lightweight and portable environments that can run on any system that supports Docker. A Dockerfile contains various instructions for building a Docker image. And these instructions contains the commands to install various dependencies, copy files into the image, set environment variables, and configure the runtime environment. Once a Dockerfile is created, it can be used with the `docker build` command to build an docker image. The dockerfiles are the kind of essential tools that are used for building and deploying applications into the docker containers.

## Format of Dockerfile

`FROM -> To pull image.`

`RUN -> To run command.`

`EXPOSE -> To open port.`

`COPY -> to сору file & directories from host to image.`

`ENV -> to set environment variable.`

`CMD -> specifies the command to run when a container is running using the docker image.`

`ENTRY POINT -> Specifies the command to run when a container is run from passed in image but allows additional argument to be passed in.`

`ADD → copies files from host to image, downloads zip/tar files from given link & extracts it automatically.`

`ARG → Defines variables that passed to container, while building image.`

`VOLUME→ create volume inside in container for sharing one container's volume to another.`

`WORKDIR -> to set working directory.`

`MAINTAINER → To set name email of author/user.`

`LABEL -> To add metadata.`

`USER -> To set user.`

`HEALTH CHECK →To specifies path for health check.`

`SHELL -> specifies shell to be used to run commands.`

`STOP SIGNAL→ specifies the signal to sent container when want to stop container gracefully.`

### Dockerfile Examples

1. Dockerfile for Simple Python Application:
    
    ```dockerfile
    # Use an existing Python image as a base
    FROM python:3.9-slim
    
    # Set the working directory inside the container
    WORKDIR /app
    
    # Copy the current directory contents into the container at /app
    COPY . /app
    
    # Install any needed dependencies specified in requirements.txt
    RUN pip install --no-cache-dir -r requirements.txt
    
    # Run app.py when the container launches
    CMD ["python", "app.py"]
    ```
    
    **Explanation:**
    
    1. `FROM python:3.9-slim`: This line of the dockerfile contains the base image to use, which is an existing Python 3.9 slim image.
        
    2. `WORKDIR /app`: Sets the working directory inside the container to the location `/app`.
        
    3. `COPY . /app`: Copies the current directory's contents into the new `/app` directory contained in the docker container.
        
    4. `RUN pip install --no-cache-dir -r requirements.txt`: Installs dependencies specified in `requirements.txt` file.
        
    5. `CMD ["python", "`[`app.py`](http://app.py)`"]`: Contains the commands to run when the docker container starts, which in this case is to execute [`app.py`](http://app.py) file using Python.
        
2. Dockerfile for Node.js Application with Build Stage:
    
    ```dockerfile
    # Stage 1: Build the application
    FROM node:14 AS build
    
    WORKDIR /app
    
    COPY package*.json ./
    
    RUN npm install
    
    COPY . .
    
    RUN npm run build
    
    # Stage 2: Create a lightweight image
    FROM nginx:alpine
    
    COPY --from=build /app/build /usr/share/nginx/html
    
    EXPOSE 80
    
    CMD ["nginx", "-g", "daemon off;"]
    ```
    
    **Explanation:** The above Dockerfile is divided into 2 steps and each step contains some commands such as:
    
    **a) Stage 1:** It Builds the Node.js application.
    
    1. `FROM node:14 AS build`: Uses the Node.js 14 image as a base with an alias `build`.
        
    2. `WORKDIR /app`: Sets the working directory.
        
    3. `COPY package*.json ./`: Copies and installs dependencies.
        
    4. `RUN npm install`: It also copies and installs dependencies.
        
    5. `COPY . .`: Copies application code and builds it.
        
    6. `RUN npm run build`: It also copies application code and builds it.
        
        **b) Stage 2:** Creates a lightweight docker image for serving the NodeJS application.
        
        1. `FROM nginx:alpine`: Uses the Nginx Alpine image.
            
        2. `COPY --from=build /app/build /usr/share/nginx/html`: It copies the built application from the previous stage.
            
        3. `EXPOSE 80`: Exposes the NodeJS application to port 80.
            
        4. `CMD ["nginx", "-g", "daemon off;"]`: Runs Nginx in the beginning.
            
3. Dockerfile for Static Website:
    
    ```dockerfile
    # Use a lightweight base image
    FROM nginx:alpine
    
    # Copy static HTML files to the default Nginx web server directory
    COPY . /usr/share/nginx/html
    
    # Expose port 80 to allow outside access
    EXPOSE 80
    
    # Command to start Nginx server in the foreground
    CMD ["nginx", "-g", "daemon off;"]
    ```
    
    **Explanation:**
    
    1. This Dockerfile uses a Nginx docker image based on Alpine Linux.
        
    2. `COPY . /usr/share/nginx/html`: it copies the static HTML files (e.g., index.html, CSS, JavaScript) to the default Nginx web server directory.
        
    3. `EXPOSE 80`: Exposes to port 80 to allow outside access to the static website.
        
    4. `CMD ["nginx", "-g", "daemon off;"]`: It starts the Nginx server in the beginning so that the Docker can manage its further process.
        
4. Dockerfile for Spring Boot Application:
    
    ```dockerfile
    FROM adoptopenjdk/openjdk11:alpine-jre
    
    WORKDIR /app
    
    COPY build/libs/*.jar app.jar
    
    EXPOSE 8080
    
    CMD ["java", "-jar", "app.jar"]
    ```
    
    **Explanation:**
    
    1. Uses an OpenJDK image for the Java applications.
        
    2. Then it copies the Spring Boot executable JAR files into the docker container.
        
    3. Exposes to port 8080 for the Spring Boot application.
        
5. Dockerfile for PHP Application:
    
    ```dockerfile
    FROM php:8.0-apache
    
    COPY src/ /var/www/html/
    
    EXPOSE 80
    ```
    
    **Explanation:**
    
    1. In this dockerfile it uses the official PHP Apache image.
        
    2. Copies PHP application source files or codes into the docker container's web root directory.
        
    3. Exposes to port 80 for serving HTTP traffic.
        
6. Dockerfile for Static Website with React:
    
    ```dockerfile
    FROM node:14 AS builder
    
    WORKDIR /app
    
    COPY . .
    
    RUN npm install
    
    RUN npm run build
    
    FROM nginx:latest
    
    COPY --from=builder /app/build/ /usr/share/nginx/html
    
    EXPOSE 80
    ```
    
    **Explanation:**
    
    1. This Dockerfile uses a multi-stage build for building a React application.
        
    2. First stage builds the React application.
        
    3. Second stage uses the Nginx image and copies the built static files into the Nginx's HTML directory.
        
7. Dockerfile for M**y**SQL Database\*\*:\*\*
    
    ```dockerfile
    FROM mysql:latest
    
    ENV MYSQL_ROOT_PASSWORD=Vij@y@006
    ENV MYSQL_DATABASE=mysqldb
    ENV MYSQL_USER=vijaysingh
    ENV MYSQL_PASSWORD=vijaysingh006
    
    EXPOSE 3306
    ```
    
    **Explanation:**
    
    1. This above Dockerfile uses the official MySQL image.
        
    2. Then, it sets the environment variables for configuring MySQL root password, database name, user, and password.
        
    3. Exposes to port 3306 for MySQL connections.
        

Above are the few examples of Dockerfiles that can be used to carryout the various tasks. And these examples demonstrate how Dockerfiles are used to define the environment and dependencies for various types of applications.

## Command for creating the Docker Image using the Dockerfile:

1. Command used for creating the Docker Image using the Dockerfile is:
    
    ```dockerfile
    $ docker build -t <image name> .
    ```
    
2. Command used for creating the Docker Image with some arguments using the Dockerfile is:
    
    <mark>Suppose there is a scenario, where you created a OTT platform website like:- Netflix, Amazon Prime, etc. and you want to store some movies in the database of that website but on the temporary basis so that some movies will get visible when you open that website. So, for that you can you API and you can build Docker Image using the Dockerfile by passing a build argument in docker image building command like:</mark>
    
    ```plaintext
    $ docker build --build-arg OMDB_V3_API_KEY=<your-API-key> -t <image name> .
    ```
    
3. Command for building a Docker Container using Docker Image:
    
    ```plaintext
    $ docker run -d -p <port-on-host-machine-mapped-to>:<port-inside-container> <image name>
    
    //exmaple
    $ docker run -d -p 3000:3000 <image name>
    ```
    
4. Command for Tagging a Docker Image:
    
    ```plaintext
    $ docker tag <image name>:latest <dockerhub-username>/<image name>:latest
    ```
    
5. Command for pushing the Docker Image to DockerHub:
    
    ```plaintext
    $ docker push <dockerhub-username>/<image name>:latest
    ```
    
6. Command to view the logs of a running Docker Container:
    
    ```plaintext
    $ docker logs 1b804a8a6e946f67a71e6dbd9c8f2f32f78594f11c37b33e71f8f4d50f55f18e
    Server running at http://localhost:3000/
    ```
    

### Sample Output of building a Docker Image:

```plaintext
$ docker build -t myapp .
Sending build context to Docker daemon  4.82 kB
Step 1/5 : FROM node:14
 ---> 05310d03a1e8
Step 2/5 : WORKDIR /app
 ---> Using cache
 ---> 23d26d931e24
Step 3/5 : COPY package*.json ./
 ---> Using cache
 ---> 02a015052e5a
Step 4/5 : RUN npm install
 ---> Using cache
 ---> 7a5b46d1312c
Step 5/5 : COPY . .
 ---> Using cache
 ---> 5dbd36f1ef39
Successfully built 5dbd36f1ef39
Successfully tagged myapp:latest
```

Sample Output of containerizing the above created Docker Image and map it to the PORT 3000:

```plaintext
$ docker run -d -p 3000:3000 myapp
1b804a8a6e946f67a71e6dbd9c8f2f32f78594f11c37b33e71f8f4d50f55f18e
```

Sample Output to view running Docker Container:

```dockerfile
$ docker ps
CONTAINER ID   IMAGE         COMMAND                  CREATED         STATUS         PORTS                    NAMES
cba9876zyxw   myapp:latest   "nginx -g 'daemon of…"   2 minutes ago   Up 2 minutes   0.0.0.0:3000->3000/tcp   myapp-container
```

Sample Output of tagging the Docker Image:

```plaintext
$ docker tag myapp:latest <dockerhub-username>/myapp:latest
```

Sample Output for pushing the Docker Image to DockerHub:

```plaintext
$ docker push <dockerhub-username>/myapp:latest
The push refers to repository [docker.io/username/myapp]
abcd1234efgh: Pushed
latest: digest: sha256:5678abcdefgh9101112ijklmnopqrstuv verified
```

Sample Output of Verifying whether a Docker Image pushed to DockerHub or not:

```dockerfile
$ docker images
REPOSITORY         TAG        IMAGE ID       CREATED         SIZE
myapp              latest     abcd1234efgh   3 minutes ago   123MB
username/myapp     latest     abcd1234efgh   3 minutes ago   123MB
```

Sample Output of the above created `myapp` Docker Container if you want to view the Logs of `myapp` Docker Container: (optional)

```plaintext
$ docker logs 1b804a8a6e946f67a71e6dbd9c8f2f32f78594f11c37b33e71f8f4d50f55f18e
Server running at http://localhost:3000/
```