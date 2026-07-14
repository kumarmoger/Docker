=============
Dockerfile
=============

=> Dockerfile contains set of instructions to build docker image.

		Filename : Dockerfile

=> Inside dockerfile we will specify below things

		1) What Dependencies Required

		2) Where is project code

		3) Project execution process

=> To write dockerfile we will use below keywords

		1) FROM
		2) MAINTAINER
		3) RUN
		4) CMD
		5) COPY
		6) ADD
		7) WORKDIR
		8) EXPOSE
		9) ENTRYPOINT
 Dockerfile Keywords Explained in Detail

A Dockerfile is a text file that contains instructions to build a Docker image. Docker executes these instructions from top to bottom, creating image layers.

1) FROM
Purpose

The FROM instruction specifies the base image for your Docker image. Every Dockerfile must start with a FROM instruction (except advanced multi-stage builds).

Think of it as the operating system or runtime on which your application will run.

Syntax
FROM <image_name>:<tag>
Examples

Ubuntu Image

FROM ubuntu:22.04

Java Application

FROM openjdk:17-jdk

Node.js Application

FROM node:20

Python Application

FROM python:3.12
Real Project Example

For a Java Spring Boot application:

FROM eclipse-temurin:17-jdk

This image already contains Java 17.

2) MAINTAINER
Purpose

Used to specify the image author's details.

Syntax
MAINTAINER Kumar Moger
Example
MAINTAINER kumar@example.com
Note

MAINTAINER is deprecated.

Nowadays Docker recommends using labels.

Instead use:

LABEL maintainer="kumar@example.com"
Real Project
LABEL maintainer="devops-team@company.com"
3) RUN
Purpose

RUN executes commands while building the Docker image.

Every RUN instruction creates a new image layer.

Syntax
RUN command
Example

Install Apache

RUN apt update
RUN apt install apache2 -y

Better way

RUN apt update && \
    apt install apache2 -y
Install Java
RUN apt update && apt install openjdk-17-jdk -y
Real Project Example

Install Maven

RUN apt-get update && \
    apt-get install -y maven
4) CMD
Purpose

Specifies the default command executed when the container starts.

Only one CMD should exist in a Dockerfile.

If multiple CMDs are written, only the last one is used.

Syntax
CMD ["command","arg1","arg2"]
Example
CMD ["java","-jar","app.jar"]

Python

CMD ["python","app.py"]

Ubuntu

CMD ["bash"]
Difference

CMD executes when the container starts, not during image build.

5) COPY
Purpose

Copies files from the local machine into the Docker image.

Syntax
COPY source destination
Example
COPY app.jar /app/

Copy everything

COPY . /app
Real Project
WORKDIR /app

COPY target/myapp.jar .
6) ADD
Purpose

ADD works like COPY but provides additional features.

It can:

Copy files
Extract compressed files automatically
Download files from URLs (not recommended)
Syntax
ADD source destination
Example

Extract tar file

ADD app.tar.gz /opt/

Docker automatically extracts it.

Download URL
ADD https://example.com/file.zip /tmp/

Not recommended.

Instead use

RUN curl -O https://example.com/file.zip
Difference

COPY

COPY app.jar /app/

ADD

ADD app.tar.gz /opt/
COPY vs ADD
COPY	ADD
Copies files	Copies files
Faster	Slightly slower
Doesn't extract archives	Extracts tar files automatically
Doesn't download URLs	Can download URLs
Recommended	Use only when needed

Interview Answer:

Use COPY whenever possible. Use ADD only if you need automatic archive extraction.

7) WORKDIR
Purpose

Sets the working directory inside the container.

After setting WORKDIR, all subsequent commands execute from this directory.

Syntax
WORKDIR /app
Example
WORKDIR /app

COPY . .

RUN mvn clean package

Without WORKDIR

RUN cd /app
RUN mvn clean package

This won't work as expected because each RUN executes in a separate layer.

WORKDIR solves this problem.

8) EXPOSE
Purpose

Documents the network port the container listens on.

It does not publish the port automatically.

Syntax
EXPOSE 8080
Example

Tomcat

EXPOSE 8080

Nginx

EXPOSE 80

Spring Boot

EXPOSE 8080

Container still needs:

docker run -p 8080:8080 image
9) ENTRYPOINT
Purpose

Defines the main executable that always runs when the container starts.

Unlike CMD, ENTRYPOINT cannot be easily overridden by passing another command.

Syntax
ENTRYPOINT ["java","-jar","app.jar"]
Example
ENTRYPOINT ["python","app.py"]

Java

ENTRYPOINT ["java","-jar","myapp.jar"]
CMD vs ENTRYPOINT
CMD	ENTRYPOINT
Default command	Fixed executable
Can be overridden	Hard to override
Optional	Used for the main application
Provides default arguments	Defines the main process
Example

Dockerfile

ENTRYPOINT ["ping"]
CMD ["google.com"]

Run

docker run ping-image

Output

ping google.com

Override CMD

docker run ping-image yahoo.com

Output

ping yahoo.com

Override ENTRYPOINT

docker run --entrypoint bash ping-image
Complete Dockerfile Example (Java Spring Boot)
FROM eclipse-temurin:17-jdk

LABEL maintainer="kumar@example.com"

WORKDIR /app

COPY target/springboot-app.jar app.jar

EXPOSE 8080

ENTRYPOINT ["java","-jar","app.jar"]
Dockerfile Build Process
Dockerfile
     │
     ▼
FROM ubuntu
     │
RUN apt update
     │
RUN apt install java
     │
COPY app.jar
     │
WORKDIR /app
     │
EXPOSE 8080
     │
ENTRYPOINT java -jar app.jar
     │
     ▼
Docker Image
     │
docker run
     ▼
Container
Interview Questions & Answers
Q1. What is the difference between RUN, CMD, and ENTRYPOINT?
RUN: Executes commands while building the image (e.g., installing packages).
CMD: Specifies the default command or arguments when the container starts; can be overridden.
ENTRYPOINT: Defines the main executable for the container; generally not overridden unless explicitly using --entrypoint.
Q2. Why is WORKDIR preferred over RUN cd?

Because each RUN instruction creates a new layer, directory changes made with cd do not persist to the next instruction. WORKDIR permanently sets the working directory for all following instructions.

Q3. Why is COPY preferred over ADD?

COPY is simpler, more predictable, and follows best practices. Use ADD only when you specifically need features like automatic extraction of local tar archives.

Q4. Does EXPOSE publish the port?

No. EXPOSE only documents the intended listening port inside the container. To make it accessible from the host, you must use port mapping, for example:

docker run -p 8080:8080 my-image
Q5. Can a Dockerfile have multiple CMD instructions?

Yes, but only the last CMD is effective. Any earlier CMD instructions are ignored.

Best Practices
Use a small base image (for example, Alpine-based images when suitable).
Prefer LABEL instead of the deprecated MAINTAINER.
Combine related RUN commands to reduce image layers.
Use COPY instead of ADD unless you need ADD's extra features.
Set a WORKDIR instead of relying on RUN cd.
Use ENTRYPOINT for the main application and CMD for default arguments.
Keep the image lightweight by removing unnecessary files and caches during the build.