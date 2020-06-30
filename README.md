# Docker-tutorial

Docker is a containerization platform that packages your application and all its dependencies together in the form of Containers to ensure that 
your application works seamlessly in any environment and can be easily shipped to run on other machines.

Docker compose
--------------
Docker Compose is a YAML file which contains details about the services, networks, and volumes for setting up the Docker application. So, you can use Docker Compose to create separate containers, host them and get them to communicate with each other. Each container will expose a port for communicating with other containers.
 
Docker Swarm
-------------
Docker Swarm is a technique to create and maintain a cluster of Docker Engines. The Docker engines can be hosted on different nodes, and these nodes, which are in remote locations, form a Cluster when connected in Swarm mode.

Installing docker on windows:
----------------------------
-> Enable Hyper-v in control panel
 
  Control panel -> Programs and features -> Turn Windows features on or off -> Enable Hyper-v
   
-> Install docker from docker website.
 
  prereq : Windows 10, 64bit
	
-> Run following commands in command prompt for sanity check:
 
      docker version -> gives version
   
      docker info -> info
 
-> Installing docker gives both client and daemon (docker server)

-> Client makes API calls to Daemon. Daemon implements the docker remote APIs.

 Docker commands:
 ---------------
 
      docker images -> lists all docker images present in local
      
      To build docker image, use docker build command as shown below
      docker build -t <image-name> .
      
      To clear the cache and build the image as fresh use --no-cache flag as shown below
      docker build --no-cache -t <image-name> .

      docker run -> to run a new container

      docker ps -> To see running and stopped containers

      docker images -> To see info about docker images
      
      docker pull image-name -> pulls image from docker hub (docker registry)

      docker rmi image-name:version -> removes image with mentioned version
      eg: docker rmi ubuntu:14:4 -> this removes ubuntu image with version 14.4 which we pulled from registry.
      
Docker commandline reference :

https://docs.docker.com/engine/reference/commandline/version/

Dockerizing Spring boot application
-----------------------------------
Lets say we have a spring boot application which uses MySQL as its database. Then inorder to dockerize this application we need to create two images. One for application and one for MySQL. To run the application either we have to combine these two containers and run it using run command or we can use "Docker compose" to spin up the application with mutiple containers. Docker compose file should contain details about these images and ports at which these containers are running.

If you are not using Docker compose, manually we have to create image for MySQL and use run command to link application container with MySQL container. To create MySQL docker container use below link

http://www.myjavablog.com/2018/08/31/connecting-to-mysql-docker-container/

If you want to use docker compose, then we have to create image for only application. For MySQL, we can specify details in docker-compose file. Docker compose will pull the base image for MySQL and creates container which is running from the base image.

while creating mysql container we specify our custom name. That name we should specify in application.properties for datasource instead of localhost.

To run the application using docker compose, use below command
      
      docker-compose up
            
if u see error saying communication link failure (connect exception related to mysql db) i.e., maybe mysql container is not started. since application is depends on mysql container we are getting this error.

So start the mysql container first. for that use below command

    docker-compose start docker-mysql 
    here docker-mysql is mysql image

then to start application again run up command like below

    docker-compose up --build

this time server will start

Use below links to know more about dockerizing spring boot app:

http://myjavablog.com/2018/08/21/dockerizing-a-spring-boot-with-mysql-application/

https://www.callicoder.com/spring-boot-docker-example/

for data persistence using docker volume use below links

https://docs.docker.com/storage/volumes/


Docker online playground for practice:
-------------------------------------
1. Play with docker classroom

	https://training.play-with-docker.com/dev-stage1/
	
2. https://labs.play-with-docker.com/p/bq7bp4iosm4g008jrj70#bq7bp4io_bq7bpldim9m00088661g

	run following command
	
	docker run -d -p 80:80 dockersamples/101-tutorial
	
	http://ip172-18-0-44-bq7bp4iosm4g008jrj70-80.direct.labs.play-with-docker.com/tutorial/ -> this gives information about docker
	
3. katacode playground

	https://www.katacoda.com/courses/docker/2
  
  
      
