* Project #1을 발전 시킴
* 서로 다른 Docker 이미지를 2종류 이상 만듬 (최소 2종류)
* 서로 다른 Docker 이미지들은 실행시, 서로 통신을 하여 무언가를 주고 받음 (무엇이든 상관없음)
* 만든 Docker 이미지들을 Docker Hub에 업로드 함
* 업로드한 Docker Hub의 URL 들을 저장한 텍스트 화일을 만들고 화일 이름을 학번.txt로 저장 함

Docker image를 2종류 이상 만들기
두개 이상의 image가 포함이 되야되는 형태. dockercompose파일을 만들어서 거기에 두 개 이상의 서비스,
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