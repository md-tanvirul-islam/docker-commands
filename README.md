# My Docker Journey
1. What is a Dockerfile?
Ans: A Dockerfile contains instructions for building an image.
2. List Dockerfile instructions:
    * FROM : to fetch based image from DockerHub. 
    * WORKDIR : to set certain directory as the working directory in the based image filesystem. All the following commands will be executed in this directory.
    * COPY : to copy file and directory from the host machine.
    * ADD : to add file and directory from the host machine.
    * RUN: to execute any system(linux/windows) command.
    * ENV : to setup environnement variable.
    * EXPOSE : to tell docker a container is starting in a given port.
    * USER : to specify the user who should run the application. Typically a user with limited privileges. 
    * CMD
    * ENTRYPOINT : to specify commands to execute when starting a container.
