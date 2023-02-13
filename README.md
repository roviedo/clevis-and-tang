# Clevis and Tang

### Prerequisites
  You can get Docker https://docs.docker.com/get-docker/

### Steps to run this project

#### To setup Clevis
    cd clevis
    sudo docker build -t clevis-client .
    sudo docker run -it clevis-client bash


#### To setup Tang
  * Run the following from your shell
      ```
      $ docker run -d -p 3000:80/tcp -h tang-container --privileged=true tang-fedora /usr/sbin/init
      ```
  * Once inside docker container run the following
      ```
      $ systemctl enable tangd.socket --now
      ```

#### To setup Clevis Ubuntu Server VM

  * Download and instal [VirtualBox](https://www.virtualbox.org/)
  * Download [Ubuntu Server](https://ubuntu.com/download/server) of version of interest
  * Open VirtualBox app, click new and find your downloaded ISO image and follow installation process.
  * Make sure that when prompt to add LUKS encryption, check it and enter desired password
  * Once VM is installed and you are in your OS, do `sudo apt-get install clevis`
  * If you have Tang running in a docker container with port 3000, you can do the following
      ```
      curl http://MY_COMPUTER_IP:3000/adv
      ```
  * From the step above you should see a payload JSON
  * If steps above successful, you can now follow steps to bind with Clevis and Tang

#### Steps to bind Clevis and Tang