=======================================================
Running Real-world applications using docker images
=======================================================

### public docker image name (java springboot app) : ashokit/spring-boot-rest-api

docker pull ashokit/spring-boot-rest-api

docker run ashokit/spring-boot-rest-api

docker run -d ashokit/spring-boot-rest-api

Syntax : docker run -d -p <host-port>:<container-port> ashokit/spring-boot-rest-api

docker run -d -p 9090:9090 ashokit/spring-boot-rest-api

Note: Host port number we need to enable in ec2-vm security group inbound rules to allow the traffic.

Note: To access application running in the container we will use below URL

## Java App URL : http://host-public-ip:host-port/welcome/{name}


### public docker image name (python app) : ashokit/python-flask-app

docker pull ashokit/python-flask-app

docker run -d -p 5000:5000 ashokit/python-flask-app

## Python App URL : http://host-public-ip:host-port/

Note: Host port number we need to enable in ec2-vm security group inbound rules to allow the traffic.