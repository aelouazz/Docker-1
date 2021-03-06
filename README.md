# Docker-1

**Author: [aelouazz](https://www.github.com/aelouazz)**

### Now, i am thinking containers!!

---

# Intro

The aim of the Docker-1 project is to be able handle docker and docker-machine, the
bases to understand the idea of containerization of services. I see this project as
an initiation.

---

## all important commands:

[**https://docs.docker.com/engine/reference/commandline/docker/**](https://docs.docker.com/engine/reference/commandline/docker/)

# How to Docker

- [ ]  **1- Create a virtual machine with docker-machine using the virtualbox driver, and named Char**

        docker-machine create --driver virtualbox Char

    **--driver** flag to indicate which provider (VirtualBox, DigitalOcean, AWS, etc.) the machine should be created on

    **char** is an argument to indicate the name of the created machine

    > to check result use:

        docker-machine ls

- [ ]  **2- Get the IP address of the Char virtual machine**

        docker-machine ip Char

    **Docummentation: docker-machine ip**

        # To get the IP address of one or more machines:
        
        $ docker-machine ip dev
        192.168.99.104
        
        $ docker-machine ip dev dev2
        192.168.99.104
        192.168.99.105

- [ ]  **3- Define the variables needed by your virtual machine Char in the general env of your
terminal, so that you can run the docker ps command without errors. You have
to fix all four environment variables with one command, without using shell’s builtin to set these variables by hand**

        eval $(docker-machine env Char)

    Set environment variables to dictate that **docker** should run a command against a particular machine.

        # **for more infos run:** 
        docker-machine env --help
        # **to unset the variables:**
        eval $(docker-machine env -u)

    > **More infos:** [https://docs.docker.com/v17.09/machine/reference/env/](https://docs.docker.com/v17.09/machine/reference/env/)

- [ ]  **4- Get the hello-world container from the Docker Hub, where it’s available**

        docker pull hello-world
        # **pull** pulls an image or a repository from a registry
        
        # To check results:
        docker image ls

    > **More infos:** [https://ropenscilabs.github.io/r-docker-tutorial/04-Dockerhub.html](https://ropenscilabs.github.io/r-docker-tutorial/04-Dockerhub.html)

- [ ]  **5- Launch the hello-world container, and make sure that it prints its welcome message, then leaves it**

        # As easy as:
        docker run hello-world

    The **docker run** command must specify an IMAGE to derive the container from

    > **More infos:** [https://docs.docker.com/engine/reference/run/](https://docs.docker.com/engine/reference/run/)

- [ ]  **6- Launch an nginx container, available on Docker Hub, as a background task. It should be named overlord, be able to restart on its own, and have its 80 port attached to the 5000 port of Char.** You can check that your container functions properly by visiting http://&lt;ip-de-char&gt;:5000 on your web browser.

        docker run -d -p 5000:80 --name overlord --restart=always nginx

    **-d** or **--detach**           Run container in background and print container ID

    **--name** [name]          Assign a name to the container

    **-p** or **--publish list**    Publish a container's port(s) to the host

    **-p** is a ports mapping [HOST PORT]:[CONTAINER PORT]


    **--restart** to specify a container’s restart policy. A restart policy controls whether the Docker daemon restarts a container after exit

    > **More infos:** [https://docs.docker.com/engine/reference/run/#restart-policies---restart](https://docs.docker.com/engine/reference/run/#restart-policies---restart)

- [ ]  **7- Get the internal IP address of the overlord container without starting its shell and in one command**

        docker inspect -f '{{.NetworkSettings.IPAddress}}' overlord

    **inspect**   Returns low-level information on Docker objects

    **-f**             Formats the output using the given Go template

    > **More infos:** [https://docs.docker.com/engine/reference/commandline/inspect/](https://docs.docker.com/engine/reference/commandline/inspect/)

- [ ]  **8- Launch a shell from an alpine container, and make sure that you can interact directly with the container via your terminal, and that the container deletes itself once the shell’s execution is done**

        docker run -it --rm alpine /bin/sh

    **-i** or **--interactive**     Keep STDIN open even if not attached.

    **-t** or **--tty**                 Allocate a pseudo-TTY.

    **--rm**                         Automatically remove the container when it exits

    > **More infos:** [http://containertutorials.com/alpine/get_started.html](http://containertutorials.com/alpine/get_started.html)

- [ ]  **9- From the shell of a debian container, install via the container’s package manager everything you need to compile C source code and push it onto a git repo (of course, make sure before that the package manager and the packages already in the container are updated).** For this exercise, you should only specify the commands to be run directly in the container

        apt-get update
        apt-get upgrade -y
        apt-get install build-essential git -y

    we need to lunch the container first using: "**docker run -it --rm ubuntu**"

- [ ]  **10- Create a volume named hatchery**

        docker volume create --name hatchery

    **to list all volumes:** "docker volume ls"

    > **More infos:** [https://docs.docker.com/engine/reference/commandline/volume_create/](https://docs.docker.com/engine/reference/commandline/volume_create/)
