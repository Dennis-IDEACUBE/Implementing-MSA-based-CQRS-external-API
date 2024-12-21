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

### Settings Visual Studio Code over SSH Key

     ssh-keygen -t rsa -b 4096
     cd ~/.ssh
     cat id_rsa.pub >> ~/.ssh/authorized_keys
     cat authorized_keys
     cat id_rsa 
     copy id_rsa on Host Windows(C:\Users\사용자\.ssh)      
