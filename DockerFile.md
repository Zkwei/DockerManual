# Docker Manual Ubuntu #

#### Docker Community Install ####

ref: ```https://docs.docker.com/install/linux/docker-ce/ubuntu/```

* Uninstall old versions 

    ```shell
    $ sudo apt-get remove docker docker-engine docker.io containerd runc
    ```

* Install Docker Engine - Community

  * Install using the repository
    * SET UP THE REPOSITORY
    1. Update the ```apt``` packet Index
   
        ```shell
        $ sudo apt-get update
        ```

    2. Install packets allow ```apt``` to use a repository over HTTPS:
        ```shell
        $ sudo apt-get install \
            apt-transport-https \
            ca-certificates \
            curl \
            gnupg-agent \
            software-properties-common
        ```
    3. Add Docker’s official GPG key and verify the fingerprint ``` 9DC8 5822 9FC7 DD38 854A E2D8 8D81 803C 0EBF CD88 ```, by the last 8 characters:

        ```shell
        $ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
        ```

        ```shell
        $ sudo apt-key fingerprint 0EBFCD88
    
        pub   rsa4096 2017-02-22 [SCEA]
            9DC8 5822 9FC7 DD38 854A  E2D8 8D81 803C 0EBF CD88
        uid           [ unknown] Docker Release (CE deb) <docker@docker.com>
        sub   rsa4096 2017-02-22 [S]
        ```

    4. Setup the stable repository of ``` x86_64/amd64 ```:
        ```shell
            $ sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
        ```

    * INSTALL DOCKER ENGINE - COMMUNITY
  
    1. Update the ```apt``` package index.

        ```shell
        $ sudo apt-get update
        ```

    2. Install the latest version of Docker Engine - Community and containerd, or go to the next step to install a specific version: 

        ```shell
        $ sudo apt-get install docker-ce docker-ce-cli containerd.io
        ```
    3. To install a specific version of Docker Engine - Community, list the available versions in the repo, then select and install:

        a. List the versions available in your repo: 
        
        ```shell
        $ apt-cache madison docker-ce

        docker-ce | 5:18.09.1~3-0~ubuntu-xenial | https://download.docker.com/linux/ubuntu  xenial/stable amd64 Packages
        docker-ce | 5:18.09.0~3-0~ubuntu-xenial | https://download.docker.com/linux/ubuntu  xenial/stable amd64 Packages
        docker-ce | 18.06.1~ce~3-0~ubuntu       | https://download.docker.com/linux/ubuntu  xenial/stable amd64 Packages
        docker-ce | 18.06.0~ce~3-0~ubuntu       | https://download.docker.com/linux/ubuntu  xenial/stable amd64 Packages
        ...
        ```
        b. Install a specific version using the version string from the second column, for example, ```5:18.09.1~3-0~ubuntu-xenial```.

        ```shell
        $ sudo apt-get install docker-ce=<VERSION_STRING> docker-ce-cli=<VERSION_STRING> containerd.io
        ```

    4. Verify that Docker Engine - Community is installed correctly by running the ```hello-world``` image.

        ```shell
        $ sudo docker run hello-world
        ```


#### Using Docker ####

* Get Ubuntu image

    ```shell
    $ sudo docker pull ubuntu:16.04
    ```

* Check image

    ```shell
    $ sudo docker images
    REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
    ubuntu              16.04               b9409899fe86        2 weeks ago         122MB
    hello-world         latest              fce289e99eb9        10 months ago       1.84kB
    ```

* Run a container
    * Run 

        ```shell
        $ sudo docker run -itd -p {your_port}:22 {your_image}
        ```
        
        For example:

        ```shell
        $ sudo docker run -itd -p 1234:22 ubuntu:16.04
        ```

    * Execute container

        ```shell
        $ sudo docker exec -it {your_container_name} /bin/bash
        ```

        For example:

        ```shell
        $ sudo docker run -itd -p 1234:22 ubuntu:16.04
        ```

### NOW YOU GET IN THE CONTAINER ###

#### Configurate ssh ####

  * Install ssh (root user)
    ```shell
    $ apt-get update
    $ apt-get install openssh-client
    $ apt-get install openssh-server
    ```

  * Start ssh

    ```shell
    $ /etc/init.d/ssh start
    $ ps -e|grep ssh
     3457 ?        00:00:00 sshd
    10925 ?        00:00:00 sshd
    10939 ?        00:00:00 sshd
    ```

  * Change configure

    ```shell
    $ apt-get install vim
    $ vim /etc/ssh/sshd_config
    ```

    change

    ```shell
    PermitRootLogin prohibit-password
    ```
    to 

    ```shell
    # PermitRootLogin prohibit-password
    PermitRootLogin yes
    ```
  * ssh restart

    ```shell
    $ service ssh restart
    ```

  * change password of root
  
    ```shell
    $ passwd root
    ```
### Now you can use ssh connect to docker ###

```shell
    $ ssh username@IP -p {your_port}
```

* example

    ```shell
    $ ssh root@192.168.83.2 -p 1234
    ```
