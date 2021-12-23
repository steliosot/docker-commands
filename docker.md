# 1. Commands to install docker

## Update system

    $ sudo groupadd docker

## Install docker

    $ sudo apt-get install docker.io

## Docker version

    $ sudo docker --version

## See docker information

    $ sudo docker info

# 2. Create the docker group

    $ sudo groupadd docker

## Add user (student) to docker group

    $ sudo groupadd docker
    $ sudo usermod -aG docker student
    $ newgrp docker

## Verify that it works!

    $ docker image ls

# 3. Pull and run an Ubuntu image
> Ops: Pull an image, start a container, attach to the container
> execute a command inside it, stop it, delete it

    $ docker pull ubuntu:latest

## Let's see the docker information

    $ docker info

## Let's see the images

    $ docker images

## Let's run it

    $ docker container run -it ubuntu:latest /bin/bash

> The -it makes it interactive and attaches the current shell to the container's terminal

## Inside the container

    $ ls -l
    $ ps -el

## Exit the container 

    Press Ctrl-C, followed by Ctrl-D, to detach from your connection.

## See running containers

    $ docker container ls

> CONTAINER ID   IMAGE           COMMAND       CREATED         STATUS         PORTS     NAMES
> 95a7039be942   ubuntu:latest   "/bin/bash"   8 minutes ago   Up 7 minutes             zealous_hugle

## Attach to container shell

    $ docker container exec -it zealous_hugle bash

## See container status

    $ docker container ls

## Stop container

    $ docker container stop

## See all containers (running/stopped)

    $ docker container ls --all

## Remove the container

    $ docker container rm zealous_hugle

# 

