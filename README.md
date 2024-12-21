### Implementing-MSA-based-CQRS-external-API
- Google Drive Url : https://drive.google.com/drive/folders/1URe_N0AU-ssDHbDecXjUGqQk9GPUDlux?usp=sharing

### Microservices Patterns With examples in Java(GitHub)
- https://github.com/microservices-patterns/ftgo-application

### dynamodblocal-init

      # FROM python:2.7.16-alpine3.9
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

### Settings Visual Studio Code over SSH Key

     ssh-keygen -t rsa -b 4096
     cd ~/.ssh
     cat id_rsa.pub >> ~/.ssh/authorized_keys
     cat authorized_keys
     cat id_rsa 
     copy id_rsa on Host Windows(C:\Users\사용자\.ssh)      



### Visual Stdio Code & Extensions

Install Visual Studio Code(https://code.visualstudio.com/download)

    Remote SSH - Extension
    # Create Ubunt-22.04
    # After jdk 17
    Extension Pack for Java - Extension
    Spring Boot Extension Pack - Extension

### Init

    $ sudo apt-get install zip nano vim iputils-ping git
    $ sudo apt-get install maven

### Docker

https://docs.docker.com/engine/install/ubuntu/

    # Add Docker's official GPG key:
    sudo apt-get update
    sudo apt-get install ca-certificates curl
    sudo install -m 0755 -d /etc/apt/keyrings
    sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
    sudo chmod a+r /etc/apt/keyrings/docker.asc

    # Add the repository to Apt sources:
    echo \
      "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
      $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
      sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
    sudo apt-get update

    sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
    sudo docker run hello-world

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
