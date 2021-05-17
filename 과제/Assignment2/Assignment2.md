* Project #1을 발전 시킴
* 서로 다른 Docker 이미지를 2종류 이상 만듬 (최소 2종류)
* 서로 다른 Docker 이미지들은 실행시, 서로 통신을 하여 무언가를 주고 받음 (무엇이든 상관없음)
* 만든 Docker 이미지들을 Docker Hub에 업로드 함
* 업로드한 Docker Hub의 URL 들을 저장한 텍스트 화일을 만들고 화일 이름을 학번.txt로 저장 함

Docker image를 2종류 이상 만들기
두개 이상의 image가 포d함이 되야되는 형태. dockercompose파일을 만들어서 거기에 두 개 이상의 서비스,
하나의 서비스가 하나의 이미지에 매핑되니까 결국은 두 개 이상의 서비스가 dockercompose에 있다.

```
FROM ubuntu:latest
MAINTAINER SteveLee "lclgood@khu.ac.kr"
RUN apt-get update
RUN apt-get install -y nginx
RUN echo "this is a ubuntu container"
WORKDIR /etc/nginx
CMD ["nginx", "-g", "daemon off;"]
EXPOSE 80
```

```
# Start an nginx container, give it the name 'mynginx' and run in the background
docker run --rm --name mynginx --detach nginx

# Get the IP address of the container
docker inspect mynginx | grep IPAddress

# Run busybox(a utility container). It will join the bridge network
docker run -it busybox sh

# Fetch the nginx homepage by using the container's IP address
busybox$ wget -q -O - 172.17.0.2:80


#### 학우님의 질문사항 참조^^
version: '3.7'
services:
  app:
    build: ./service-application
    env_file: ./.env
    networks:
      - webnet 
    ports:
     - "8080:8080"
    depends_on:
     - db
     - redisdb
    environment:
     - DATABASE_HOST=$DATABASE_HOST
     - PORT=$PORT
     - REDIS_HOST=$REDIS_HOST
     - COOKIE_SECRET=$COOKIE_SECRET
     - KAKAO_ID=$KAKAO_ID
     - KAKAO_SECRET=$KAKAO_SECRET
     - GITHUB_CLIENT_ID=$GITHUB_CLIENT_ID
     - GITHUB_CLIENT_SECRET=$GITHUB_CLIENT_SECRET
     - S3_ACCESS_KEY_ID=$S3_ACCESS_KEY_ID
     - S3_SECRET_ACCESS_KEY=$S3_SECRET_ACCESS_KEY
    volumes:
     - ./service-application/api:/app/api
  db:
    build: ./mysql-database
    command: --default-authentication-plugin=mysql_native_password
    restart: always
    ports:
      - 3306:3306
    volumes:
      - ./mysql-database/custom.conf:/etc/mysql/conf.d/custom.cnf
    networks: 
      - webnet
  redisdb:
    build: ./redis-database
    restart: always
    command: redis-server --requirepass $REDIS_PASSWORD --port 6379
    ports : 
      - 6379:6379
    networks: 
      - webnet
networks: 
  webnet: 
```