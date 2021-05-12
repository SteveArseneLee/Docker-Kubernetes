# Docker Compose
- A tool for defining and running multi-container docker applications

## Docker Compose Features
### Start all services
docker-compose up

### Stop all services
docker-compose down

### Scale up selected services while required
docker-compose scale

### Check of docker-compose has been installed
docker-compose
docker-compose --help
docker-compose version

```
# yml file
version: '3.7'
sevices:
 web:
  image: nginx
 database:
  image: redis
```
### create services
docker-compose up -d

### check activated services
docker-compose config
docker container ls -a & docker image ls
docker stats

### How to stop services
docker-compose down

### Create modified services using Port Mapping
docker-compose up -d
```
# yml file
version: '3.7'
sevices:
 web:
  image: nginx
  port:
   - "8000:80"
 database:
  image: redis
```

docker-compose up -d
docker contianer ls
curl http://localhost:8001
docker container exec -it {master container ID} /bin/bash
apt-get update
apt-get upgrade
apt-get -y install curl
curl http://worker1:80
curl http://worker2:80
docker-compose down

### Manager & Workers (Alpine)
docker-compose up -d --scale manager=4
docker container ls -a
docker-compose ps
docker-compose logs
docker-compose down
docker-compose run -p 9998:80 -d worker1

### Jenkins Upgrade
docker run --name jenkins-production \
--detach \
-p 50000:50000 \
-p 8080:8080 \
-v myvol-1:/var/jenkins_home \
jenkins/jenkins:2.190.1

### Execute another Jenkins
docker run --name jenkins-production-copy \
--detach \
-p 50001:50000 \
-p 8081:8080 \
-v myvol-1:/var/jenkins_home \
jenkins/jenkins:2.190.1

### Remove Volume
docker volume ls
docker volume rm {volume name}
docker volume prune