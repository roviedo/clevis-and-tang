# Clevis and Tang

### Prerequisites
  You can get [Docker](https://docs.docker.com/get-docker/)

  You can get [VirtualBox](https://www.virtualbox.org/)

### Steps to run this project

#### To setup Tang
  * Run the following from your shell
      ```
      $ docker run -d -p 3000:80/tcp -h tang-container --privileged=true tang-fedora /usr/sbin/init
      ```
  * Then run this to enter docker container
      ```
      docker exec -it <container_name> /bin/bash
      ```
  * Once inside docker container run the following
      ```
      $ systemctl enable tangd.socket --now
      ```
  * You can run `systemctl status tangd.socket` to see it running, you can then exit container.

#### To setup Clevis in Docker with Ubuntu
    cd docker_clevis_ubuntu
    sudo docker build -t clevis-client .
    sudo docker run -it clevis-client bash

  * With the Tang server running you can get your host IP and do the following.

    ```
    curl http://<MY_HOST_IP:TANG_PORT>/adv
    ```
  * If you got a payload from the above, to encrypt a string
    ```
    echo hi | clevis encrypt tang '{"url": "http://<MY_HOST_IP:TANG_PORT>:3000"}' > hi.jwe
    ```
  * Then you can decrypt the hi.jwe and get back the original string "hi", with following command.
    ```
    clevis decrypt < hi.jwe
    ```

#### To setup Clevis in Virtual Box with Ubuntu

  * Download and instal [VirtualBox](https://www.virtualbox.org/)
  * Download [Ubuntu Server](https://ubuntu.com/download/server) of version of interest
  * Open VirtualBox app, click new and find your downloaded ISO image and follow installation process.
  * Make sure that when prompt to add LUKS encryption, check it and enter desired password
  * Once VM is installed and you are in your OS, do `sudo apt-get install clevis`
  * If you have Tang running in a docker container with port 3000, you can do the following
      ```
      curl http://MY_HOST_IP:3000/adv
      ```
  * From the step above you should see a payload JSON
  * If steps above successful, you can now follow steps to bind with Clevis and Tang

#### Steps to bind Clevis and Tang
  * From the command line do `lsblk` to find your hard drive path
  * Do the following to generate adv.jws file and drop into tmp folder
      ```
      curl -sfg http://tang.srv:port/adv -o /tmp/adv.jws
      ```
  * Assuming that your path is /dev/sda3 do the following
      ```
      echo 'hello' | clevis luks bind -d /dev/sda3 tang '{"url":"http://tang.srv:port","adv":"/tmp/adv.jws"}'
      ```
  * Then do `update-initramfs -u` and then reboot `sudo reboot now`
  * Your hard drive should have unlocked and ask you only for system username/password