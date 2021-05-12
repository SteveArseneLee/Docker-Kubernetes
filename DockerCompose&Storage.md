docker-compose
docker-compose --help
docker-compose version
docker-compose up
docker-compose down
docker-compose scale

### Ubuntu OS
apt-get update
apt-get upgrade
apt-get -y install curl

### Alpine OS
apk add curl
apk add nano

curl (or web browser) http://localhost:8001
curl http://worker1:80

nano docker-compose.yml

## Docker Storage
docker volume create
docker volume prune

docker volume --help
docker volume create myvol-1
docker volume ls
docker volume inspect myvol-1

docker pull jenkins/jenkins:2.138.4
docker run -p 8080:8080 -p 50000:50000 -v myvol-1:/var/jenkins_home jenkins/jenkins:2.138.4

docker container stop {docker container ID}
docker volume ls
docker volume inspect myvol-1

docker run --name jenkins-production --detach -p 50000:50000 -p 8080:8080 -v myvol-1:/var/jenkins_home jenkins/jenkins:2.190.1

docker volume ls
docker volume rm {volume name}
docker volume prune

## Docker Machine
docker-machine --help
docker-machine --version
docker-machine version
docker-machine ls
docker-machine create --driver virtualbox myvm1
docker-machine stop myvm1
docker-machine start myvm1 (restart, if required)
docker-machine rm myvm1
docker-machine create --driver virtualbox default
docker-machine ip
docker-machine version
docker-machine inspect default
docker-machine ssh default docker version
docker run busybox echo hello world
docker-machine ssh default docker run busybox echo hello world
docker-machine ssh default docker run -d -p 4000:80 nginx
docker-machine env default
eval $(docker-machine env default)
eval $(docker-machine env -u)

