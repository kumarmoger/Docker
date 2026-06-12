================================================
Dockerizing java web app (Without SpringBoot)
================================================

=> Java web app will be packaged as "war" file

Note: Using maven build tool we will package java applications.

=> war file will be created inside project "target" directory.

=> To deploy war file we need web server (Ex: tomcat).

=> Inside tomcat server "webapps" directory we will keep war file for application execution.

######### Dockerfile to run java web app ############

FROM tomcat:latest

EXPOSE 8080

COPY target/app.war /usr/local/tomcat/webapps/

==========
Lab Task
==========

@@ Java Web App Git Repo : https://github.com/ashokitschool/maven-web-app.git

Note: Connect with Docker VM using SSH client and execute below commands

# install git client
$ sudo yum install git -y

# install maven s/w
$ sudo yum install maven -y

# clone project git repo
$ git clone https://github.com/ashokitschool/maven-web-app.git

# build maven project
$ cd maven-web-app
$ mvn clean package

# check project war file
$ ls -l target

# build docker image
$ docker build -t <img-name> .
$ docker images

# Create Docker Container
$ docker run -d -p 8080:8080 <image-name>
$ docker ps

=> Enable host port number in security group inbound rules and access our application.

		URL :: http://public-ip:8080/maven-web-app/
