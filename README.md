# Docker-Cheat-Sheet


Why do we need docker?

Due to OS incompatibility and libraries different versions, we can use docker in order to create a image that has the code, the dependencies and the configuration, and this image can be used in any environment whether it is a local machine or a production live server.

What can docker do?

Containerize applications.
Run each service with its own dependencies in a seperate container.

What is an image?

image is a lightweight, standalone, executable package of software that includes everything needed to run an application: code, runtime, system tools, system libraries and settings.

What are container?

A container is a runnable instance of an image.

=====================================================================================================

Any OS is consisted of two things:

An OS kernel that is responsible in interacting with the hardware,
A software that makes each OS different.

Docker containers all share the same linux kernel.

=====================================================================================================

Docker Commands:

1) docker run 

example: docker run nginx

2) docker ps
to list running containers

3) docker ps -a 
to list all available containers

4) docker stop <container_name>

5) docker rm <container_name>
  to remove a container
  
6) docker images

to list all available images

6) docker rmi <image>
  
  to remove an image
  
7)docker pull <image>
  
to pull an image from dockerHub
  
7) docker exec  
  
let's say i want to view the content of a specefic file inside a container 
  
example: docker exec <container_name> cat \etc\hosts
  
8) docker run:
  docker -t run:
  this is to run the container in an interactive mode since the default is non-interactive mode.
  
  docker -it:
  to run in interactive mode and attach to the terminal for exammple to pass input
  docker run <image>:<tag>
  
  to run a specific tag of an image, if no tag is specified the latest tag is the default
  this is by default will the container in an attached mode to the console
  
 docker run -d :
  
  will the container in a detached mode
  
9)docker attached <container_id>
  
to enable attach mode of any container

10)docker run -p
Port mapping
  
  docker run -p 8000:5000
  
11)docker run -v
  
volum mapping
  
let's suppose that i have container have a container called mysql
if i run:
  docker stop mysql
  docker rm mysql
  
  all the data in this container will be deleted.
  
  to persist the data in case the container is deleted we can run the following:
  
  docker run -v /opt/datadir:/var/lib/mysql mysql
  
  before the colon is external directory that will get the data inside the patch after the colon in case the container is deleted
  
  to map a 8000 in you browser for example to be 5000 inside you container

  12) docker inspect <container_name>
  
  to view more information about any container
  
  13)docker logs <container_logs>

  to view the logs of a specified container.
  
  
  ============================================================================================================
  
  Docker Environment Variables:
  
  Let assume that we want to pass an environment variable called APP_COLOR
  
  docker run -e APP_COLOR=red simple-webapp-color
  
  you can use docker inspect command to view environment variables as well.
  
  ===========================================================================================================
  
  ![image](https://user-images.githubusercontent.com/52213112/206317344-9b0d1398-b0e4-45ed-bb68-49c6f3cee33b.png)
  
  ![image](https://user-images.githubusercontent.com/52213112/206317401-f8edc2eb-c4e7-4c60-9ddf-1d5e57e76d27.png)
  
![image](https://user-images.githubusercontent.com/52213112/206317534-2158851b-e486-4ecd-aef5-b3fbcccc28f0.png)

![image](https://user-images.githubusercontent.com/52213112/206317733-5dd70a62-5a83-456f-b6e0-6f5ffcb22525.png)

![image](https://user-images.githubusercontent.com/52213112/206317942-f7e808f2-8bc5-42f3-9b8f-83bd7e2b61e1.png)

![image](https://user-images.githubusercontent.com/52213112/206318179-90f8a36b-b1d7-4bb1-aebd-86f51d0142f9.png)
  
  ![image](https://user-images.githubusercontent.com/52213112/206655256-f42d71ab-582b-4889-8ed4-890863f92faf.png)
===============================================================================================================
  
  To run an image and give another name:
  
  image name: myapp
  
  docker run --name myapp_c1 myapp

What the following does?
  -docker build -t myapp5 .
  building an image based on docker rile in the current directory and calling the image myapp5
  -docker build -t myapp2:test .
  
  running a docker file in the currency directory to build an image and give it a name and a tag

  
  -docker run --name my_container -p 4000:4000 myapp2:test
  start container with name my_container and map ports from local to container 
  
  -docker run --name my_container -p 4000:4000 -rm myapp2:test
  the -rm to remove the container once we stop later on.
===============================================================================================================
  
  Docker Volumes
  
 The purpose of using Docker volumes is to persist data outside the container so it can be backed up or shared. Docker volumes are dependent on Docker's file system     and are the preferred method of persisting data for Docker containers and services.  
  
  First off note that if you built an image based on a code and then you changed the code you to build the image again since it doesn't update automatically.
  
  with volumes we can map our local project folder to the container folder.
  using the option -v
  
  docker run --name my_container -p 4000:4000 -rm -v C:\Users:\Desktop\api:/app myapp2:test
  
  before the colon is the path of out project locally and after the colon isthe path of our container (it depends on what we specified previously)
  
  But this can make a problem that if we deleted the dependencies of a project for examples deleting node modules this is ganna be sync with container resulting of a crach of the app
  
  the solution can be as follows by adding another volume:
  
  docker run --name my_container -p 4000:4000 -rm -v C:\Users:\Desktop\api:/app -v /app/node_modules myapp2:test
  
  the second volume will map the node modules to a specific path in the container.
  
  
  =============================================================================================================================
  
  Docker Compose
  
  You can set the desired amount of containers counts, their builds, and storage designs, and then with a single set of commands you can build, run and configure all     the containers. Docker Compose is great for development, testing, and staging environments, as well as continuous integration workflows.
  
  To run docker compose file:
  
  Just run the following command:
  
  docker-compose up
  
  the following command stops and deletes the container but the images and the volumes wil remain:
  
  docker-compose down
  
  the remove all the images as well:
  
  docker-compose down --rmi all
  
  to remove the volumes as well:
  
  docker-compose down --rmi all -v
  
  
  
  
 
  
  
  
