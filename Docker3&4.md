#### ubuntu os installation
docker pull ubuntu
docker container run -it -d --rm --name ubuntuos ubuntu:latest
docker exec -it ubuntuos /bin/bash

### alpine os installation
docker pull alpine
docker container run -it -d --rm --name alpineos alpine:latest
docker exec -it alpineos /bin/ash

## Docker Hub 사용
```docker
# Dockerfile
From ubuntu:14.04
MAINTAINER SteveArseneLee "lclgood@khu.ac.kr"
RUN apt-get update
RUN apt-get install -y nginx
RUN echo "this is a ubuntu container"
WORKDIR /etc/nginx
CMD ["nginx", "-g", "daemon off;"]
EXPOSE 80
```
```shell
# 이때 마지막에 .을 반드시 찍어줍니다(현재 디렉토리란 뜻)
docker build --tag myubuntu:1.0 .
docker image ls
docker run --name myubuntu-nginx -d -p 4000:80 myubuntu:1.0
docker container ls
docker stats
```
