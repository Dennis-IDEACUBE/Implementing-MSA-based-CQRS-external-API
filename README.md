### Implementing-MSA-based-CQRS-external-API
- Google Drive Url : https://drive.google.com/drive/folders/1URe_N0AU-ssDHbDecXjUGqQk9GPUDlux?usp=sharing

### Microservices Patterns With examples in Java(GitHub)
- https://github.com/microservices-patterns/ftgo-application

### Setting HostName & Hosts & Network

<img src="https://github.com/Dennis-IDEACUBE/Implementing-MSA-based-CQRS-external-API/blob/main/nat_custom.png?raw=true">
<img src="https://github.com/Dennis-IDEACUBE/Implementing-MSA-based-CQRS-external-API/blob/main/nat_custom2.png?raw=true">

cidr : 192.168.15.0/24
ip : 192.168.15.x
gateway : 192.168.15.1
dns : 168.126.63.1, 8.8.8.8

/etc/netplan/00-installer-config.yaml

     # This is the network config written by 'subiquity'
     network:
       ethernets:
         enp0s3:
           addresses:
           - 192.168.15.100/24 # change ip address
           nameservers:
             addresses:
             - 168.126.63.1
             - 8.8.8.8
             search: []
           routes:
           - to: default
             via: 192.168.15.1
       version: 2

sudo systemctl restart network

### ftgo app server & my app server
| Server Role             | Server Hostname           | Specs                                             | IP Address     | Host Port |
| ----------------------- | ------------------------- | ------------------------------------------------- | -------------- | --------- |
| ftgo app server         | ftgo                      | 2 vCPU, 8 GB RAM, 500GB Disk                      | 192.168.15.100  | 22       |
| my app server           | myserver                  | 2 vCPU, 8 GB RAM, 500GB Disk                      | 192.168.15.101  | 23       |

### Init & Java

    $ sudo apt-get install zip nano vim iputils-ping git

    $ sudo apt update
    $ sudo apt install openjdk-17(또는 8)-jdk
    $ java -version
    $ javac -version
    $ nano .bashrc
    export JAVA_HOME=/usr/lib/jvm/java-17(또는 8)-openjdk-amd64
    export PATH=$PATH:$JAVA_HOME
    $ echo $JAVA_HOME
    $ sudo apt-get install maven
    $ mvn -version

### Git clone
    $ git clone https://github.com/microservices-patterns/ftgo-application.git

### dynamodblocal-init(파일수정)

      # FROM python:2.7.16-alpine3.9 --> 오류 발생
      FROM python:3-alpine3.11 
      RUN pip install awscli --upgrade
      COPY create-dynamodb-tables.sh .
      COPY ftgo-order-history.json .
      COPY wait-for-dynamodblocal.sh .
      RUN chmod +x *.sh
      HEALTHCHECK --interval=10s --retries=10 --timeout=3s CMD [[ -f /tables-created ]]
      
      CMD ./wait-for-dynamodblocal.sh && ./create-dynamodb-tables.sh

### docker-compose

      sudo apt-get install docker-compose


-------------------------------------------------------------------------------------------------------------------------

### Visual Stdio Code & Extensions

Install Visual Studio Code(https://code.visualstudio.com/download)

    Remote SSH - Extension
    # Create Ubunt-22.04
    # After jdk 17
    Extension Pack for Java - Extension
    Spring Boot Extension Pack - Extension

### Settings Visual Studio Code over SSH Key

    $ ssh-keygen -t rsa -b 4096
    $ cd ~/.ssh
    $ cat id_rsa.pub >> ~/.ssh/authorized_keys
    $ cat authorized_keys
    $ cat id_rsa 
    $ copy id_rsa on Host Windows(C:\Users\사용자\.ssh)      

### Docker

https://docs.docker.com/engine/install/ubuntu/

    # Add Docker's official GPG key:
    $ sudo apt-get update
    $ sudo apt-get install ca-certificates curl
    $ sudo install -m 0755 -d /etc/apt/keyrings
    $ sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
    $ sudo chmod a+r /etc/apt/keyrings/docker.asc

    # Add the repository to Apt sources:
    $ echo \
      "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
      $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
      sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
    $ sudo apt-get update

    $ sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
    $ sudo docker run hello-world

https://docs.docker.com/engine/install/linux-postinstall/

    $ sudo groupadd docker
    $ sudo usermod -aG docker $USER
    # Logout -> Login
    $ newgrp docker
    $ docker run hello-world

    # Security Issues
    $ sudo chmod 666 /var/run/docker.sock
    
    $ docker login
    $ docker pull ubuntu:22.04
