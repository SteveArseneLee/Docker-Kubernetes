#### ubuntu os installation
docker pull ubuntu
docker container run -it -d --rm --name ubuntuos ubuntu:latest
docker exec -it ubuntuos /bin/bash

### alpine os installation
docker pull alpine
docker container run -it -d --rm --name alpineos alpine:latest
docker exec -it alpineos /bin/ash

## Dockerfile 사용
### ubuntu 설치 및 업데이트
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
### python 설치 및 업데이트
```docker
FROM python:latest
MAINTAINER SteveArseneLee "lclgood@khu.ac.kr"
COPY ./app
RUN apt-get update
RUN echo "this is a python web server container"
CMD["python", "/app/webserver.py"]
EXPOSE 9000
```
```python
import socket
HOST, PORT = '', 9000
listen_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM) listen_socket.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1) listen_socket.bind((HOST, PORT))
listen_socket.listen(1)
print ('Serving HTTP on port', PORT, '...') while True:
client_connection, client_address = listen_socket.accept() request = str(client_connection.recv(1024),'utf-8')
print (request)
http_response = """\ HTTP/1.1 200 OK
Hello world!
"""client_connection.sendall(bytes(http_response,'utf-8')) client_connection.close()
```
```shell
docker build --tag mywebserver:1.0 .
docker image ls
docker run --name mypyserver -d -p 8090:9000 mywebserver:1.0 docker container ls
docker stats
#execute web-browser & access to http://localhost:8090
```
