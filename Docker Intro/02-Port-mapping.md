========================
What is Port Mapping ?
========================

Note: By default, services running inside a Docker container are isolated and not accessible from outside.

=> Docker port mapping is the process of linking container port to host machine port.

=> It is used to allow external access to applications running inside the container.

Syntax : docker run -p <host_port>:<container_port> <image_name>

Explanation
======================================================
host_port: The port on your local machine (host).
container_port: The port on which the application is listening inside the container.
image_name: The Docker image to run.


Note: host port and container port no need to be same.
Example

If a Spring Boot application runs on port 8080 inside the container:

docker run -p 8080:8080 ashokit/spring-boot-rest-api

This means:

Host (Your Machine)          Container
localhost:8080      --->     application:8080

When you access:

http://localhost:8080

the request is forwarded to port 8080 inside the container.

Another Example
docker run -p 9000:8081 sonatype/nexus3

Here:

Host port = 9000
Container port = 8081 (Nexus listens on 8081 inside the container)

Access Nexus using:

http://localhost:9000

Docker forwards the traffic:

localhost:9000  --->  container:8081
Detached Mode

Typically, you'll run containers in the background:

docker run -d -p 8080:8080 --name springapp ashokit/spring-boot-rest-api
-d = detached mode
--name springapp = container name
-p 8080:8080 = port mapping
ashokit/spring-boot-rest-api = image name

This allows users outside the container to access the application running inside it.