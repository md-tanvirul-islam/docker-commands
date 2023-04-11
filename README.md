# My Docker Journey

## Dockerfile --> build --> DockerImage --> run --> DockerContainer

1. What is a Dockerfile?
Ans: A Dockerfile contains instructions for building an image.
2. What is build context in docker?
Ans:  When docker tries to build (docker build -t new-image-name) an image from a Dockerfile, the docker client sends to the docker engine all files and folders of the directory in which the Dockerfile resides. The sibling files, folders of the Dockerfile, and Dockerfile together to make docker context/build context. Docker engine does not have access outside the docker context.
3. List Dockerfile instructions:
    * FROM : to fetch based image from DockerHub. By default, docker use latest tag to fetch image. It's better to use specific version using tag to avoid any type of undemanding behavior.
    
    * WORKDIR : to set certain directory as the working directory in the based image filesystem. All the following commands will be executed in this directory.
    Example:
    1.  WORKDIR /app (all the docker command after this, will be executed in the /app directory of docker container.)
    
    * COPY : to copy file and directory from the host machine. We can copy any files or directories from the current directory. It cannot copy anything outside the current directory. 
    Example:
    1.  COPY source(host-machine) destination(docker-image)
    2.  COPY package.json /app (if the app directory does not exist, docker will create automatically.)
    3.  COPY package.json README.md /app/ (for more than one source files, the destination must be a directory and end with a forward-slash) 
    4.  COPY package*.json /app/ (we can use wild card to match patterns)
    5.  COPY . /app/ (copying everything in the host current directory.)
    6.  WORKDIR /app
        COPY . . (coping to the /app in the docker container but using relative destination path due to WORKDIR)
    7.  COPY ["hello world.txt", "."]
    
    * ADD : to add file and directory from the host machine or url. ADD gives the option to copy using any url as extra feature than COPY instruction. If we pass compressed file, add will automatically uncompressed that file and add in the destination.
    Example: 
    1.  COPY source(host-machine) destination(docker-image)
    2.  ADD https://xyz.com/abc.json .
    3.  ADD file.zip .
    
    * RUN: to execute any system(linux/windows) command.
   
    * ENV : to setup environnement variable.
    
    * EXPOSE : to tell docker a container is starting in a given port.
    
    * USER : to specify the user who should run the application. Typically a user with limited privileges. 
    
    * CMD
    
    * ENTRYPOINT : to specify commands to execute when starting a container.
