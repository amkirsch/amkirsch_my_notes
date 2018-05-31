My Docker Notes. I will post more in future on details about Docker, Docker Compose, Docker Swarm on my blog under:
https://sysadmins.co.za/tag/docker

Get Docker:
# curl -sSL https://get.docker.io | bash

Docker Hub:

Search: 
# docker search ubuntu

Pull down the image:
# docker pull ubuntu

Create a container from an image and enter the bash shell:
# docker run -it ubuntu /bin/bash

Create a container from an image and set it to detached mode:
# docker run -itd ubuntu bash

To enter the container, get the container id:
# docker ps -lq
c3febc18e6a8

Enter the container:
# docker exec -it c3febc18e6a8  bash

Do some work:
# touch /root/somefile.txt

Commit the changes to an image:
# docker commit c3febc18e6a8 myimage:tag01

List Running Docker Containers
# docker ps

List latest Docker Container:
# docker ps -l

List All:
# docker ps -a
CONTAINER ID     IMAGE     COMMAND        CREATED        STATUS        PORTS    NAMES
f2582758af13     ubuntu    "/bin/bash"    2 hours ago    Up 2 hours             first_ubuntu

List All Container IDs:
# docker ps -a -q

Start/Stop/Attach Container
# docker start f2582758af13
# docker stop f2582758af13
# docker attach f2582758af13

Logs:
# docker logs f2582758af13

Delete Docker Container
# docker rm <ctid> --force (if the container is running)

Delete Image:
# docker rmi <image-name>

Listing Changes:
# docker diff f2582758af13

Listing Images:
# docker images

Example Docker Images:
# docker pull busybox
# docker pull alpine
# docker pull fedora


Docker 101
# docker run busybox echo 'Hello, World!'
# docker pull fedora
# docker run fedora mkdir /home/ruan -p
# docker ps -l
# docker commit c336e3afb699 my-created-dir
# docker run my-created-dir ls /home/

BUILD IMAGE FROM DOCKERFILE, LAUNCH CONTAINER FROM IMAGE
Application - Nginx:

Create file default:
# cat nginx.conf

```
server {
    root /var/www;
    index index.html index.htm;
    server_name localhost;

    location / {
        try_files $uri $uri/ /index.html;
    }
} 
```

Create file Dockerfile:

cat Dockerfile
```
FROM fideloper/docker-example:0.1

RUN echo "deb http://archive.ubuntu.com/ubuntu precise main universe" > /etc/apt/sources.list
RUN apt-get update
RUN apt-get -y install nginx

RUN echo "daemon off;" >> /etc/nginx/nginx.conf
RUN mkdir /etc/nginx/ssl
ADD default /etc/nginx/sites-available/default

EXPOSE 80

CMD ["nginx"]
```

Build new image from Dockerfile:
# docker build -t nginx-example .

# building other images
# docker -t ruanbekker/demo:v1 .

List images:
# docker images

Run app:
# docker run --name nginx_app -d nginx-example 
or:
# docker run --name apache_app -p 80:80 -d ubuntu:Apache_Server

Port Mapping:
# docker run -p 82:80 -d nginx-example
# docker run -p "127.0.0.1:80:80" -d ubuntu:Apache_Server

Stop app:
# docker stop cont-id

Share file between container and host:
# echo "Hello, world" >> /home/ruan/share/index.html

Start:
# docker run -v /home/ruan/share:/var/www:rw -p 80:80 -d nginx-example

Description:
# docker inspect a0b531aa00f4

Linking containers, needs access to each other:
# docker run -p 3306:3306 -name mysql -d some-mysql-image
# docker run -p 80:80 -link mysql:db -d some-application-image

Access container:
# docker run -it --rm name/demo:v2 /bin/bash

Dockerfile: redis:

FROM ubuntu:latest
RUN apt-get update
RUN apt-get install -y wget
RUN apt-get install -y build-essential tcl8.5
RUN wget http://download.redis.io/releases/redis-stable.tar.gz
RUN tar xzf redis-stable.tar.gz
RUN cd redis-stable && make && make install
RUN ./redis-stable/utils/install_server.sh
EXPOSE 6379
ENTRYPOINT  ["redis-server"]

Build the image:
# docker build -t myredis .

App: mongodb
# docker run --name some-mongo -d mongo
# docker run -it --link some-mongo:mongo --rm mongo sh -c 'exec mongo "$MONGO_PORT_27017_TCP_ADDR:$MONGO_PORT_27017_TCP_PORT/test"'

or: 
# docker run -i -t mongo /bin/bash


App: mysql
# docker run --name mysql01 -e MYSQL_ROOT_PASSWORD=password -d mysql
--> https://hub.docker.com/_/mysql/

App: Workdpress + MySQL
# docker run --name mysql01 -e MYSQL_ROOT_PASSWORD=password -d mysql
# docker run --name wordpress01 --link mysql01:mysql -d wordpress


== full example:
-> Dockerfile:

FROM ubuntu
MAINTAINER Ruan
RUN apt-get update -y
RUN apt-get install -y tar git curl nano wget dialog net-tools build-essential python-setuptools

docker build -t my_image .
docker run --name my_container -i -t my_image
docker ps -l

docker run -i -t my_container /bin/bash

Awesome Resources:
- https://serversforhackers.com/getting-started-with-docker
- https://scotch.io/tutorials/getting-started-with-docker
- https://hub.docker.com/explore/

Private Registry:
https://www.digitalocean.com/community/tutorials/how-to-set-up-a-private-docker-registry-on-ubuntu-14-04

Docker Usage:
http://tecadmin.net/create-list-delete-docker-containers-on-linux/

Assign port mapping
- http://stackoverflow.com/questions/19335444/how-do-i-assign-a-port-mapping-to-an-existing-docker-container
- https://forums.docker.com/t/using-localhost-for-to-access-running-container/3148/4
- https://www.digitalocean.com/community/questions/how-to-bind-multiple-domains-ports-80-and-443-to-docker-contained-applications
- http://stackoverflow.com/questions/27912917/how-to-configure-docker-port-mapping-to-use-nginx-as-an-upstream-proxy

Cheat sheet
- https://github.com/wsargent/docker-cheat-sheet
