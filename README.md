# Clevis and Tang

### Prerequisites
  You can get Docker https://docs.docker.com/get-docker/


### Steps to run this project
    cd clevis
    sudo docker build -t clevis-client .
    sudo docker run -it clevis-client bash


    cd tang
    sudo docker build -t tang-server --no-cache .
    sudo docker run -it tang-server

