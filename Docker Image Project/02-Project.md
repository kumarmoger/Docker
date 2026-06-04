### public docker image name (python app) : ashokit/python-flask-app

docker pull ashokit/python-flask-app

Syntax : docker run -d -p <host-port>:<container-port> ashokit/python-flask-app

docker run -d -p 5000:5000 ashokit/python-flask-app

## Python App URL : http://host-public-ip:host-port/

Note: Host port number we need to enable in ec2-vm security group inbound rules to allow the traffic.