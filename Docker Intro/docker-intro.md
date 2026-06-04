==================
What is Docker ?
==================

=> Docker is a free & open source software

=> Docker is used for containerization.
=> Docker is an open-source platform for running applications in containers.

Containers are lightweight, isolated environments that package applications and their dependencies.
Benefits of using Docker: portability, scalability, consistency, and resource efficiency.

Containerization = code + required softwares

=> Containerization means packaging application-code and application dependencies as single unit for execution.

=> With the help of docker we can run our application in any machine.

=> Docker will take care of dependencies installation required for application execution.

=> We can make our application portable using Docker.

====================
Docker Architecture
====================

1) Dockerfile

2) Docker Image

3) Docker Registry

4) Docker Container

=> Dockerfile is used to specify where is app code and what dependencies are required for our application execution.

Note: Using Dockerfile we can create Docker image.

=> Docker Image is a package which contains app-code + app-dependencies

=> Docker Registry is used to store docker images.

=> Docker container will be created when we run Docker image.

Note: Inside container our application will be executed.

==============
Docker Setup
=============

Git Repo For Steps : https://github.com/kumarmoger/Docker/blob/main/Intro/02-Docker-setup.md


=======================================================
Running Real-world applications using docker images
=======================================================

### public docker image name (java springboot app) : ashokit/spring-boot-rest-api

docker pull ashokit/spring-boot-rest-api

docker run ashokit/spring-boot-rest-api

docker run -d ashokit/spring-boot-rest-api
-d → Run in detached mode (background)

Syntax : docker run -d -p <host-port>:<container-port> ashokit/spring-boot-rest-api

docker run -d -p 9090:9090 ashokit/spring-boot-rest-api
-p 9090:9090 → Map host port 8080 to container port 8080.

Note: Host port number we need to enable in ec2-vm security group inbound rules to allow the traffic.

Note: To access application running in the container we will use below URL

## Java App URL : http://host-public-ip:host-port/welcome/{name}


### public docker image name (python app) : ashokit/python-flask-app

docker pull ashokit/python-flask-app

docker run -d -p 5000:5000 ashokit/python-flask-app

## Python App URL : http://host-public-ip:host-port/

Note: Host port number we need to enable in ec2-vm security group inbound rules to allow the traffic.


