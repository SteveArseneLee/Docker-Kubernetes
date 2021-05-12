### Volume
Volumes are stored in a part of the host filesystem which is managed by Docker
- Stored in a part of the host filesystem which is managed by Docker
    - Linux : /var/lib/docker/volumes/
    - Non-Docker processes should not modify this part of the filesystem
    - Volumes are the best way to persist data in Docker
- A new directory is created within Docker's storage directory on the host machine
    - Docker manages that directory's contents.
    - May be named or anonymous

### Bind mounts
Bind mounts may be stored anywhere on the host system.
- May be stored anywhere on the host system
    - may even be important system files or directories
    - Non-Docker processes on the Docker host or a Docker container can modify them at any time
- A file or directory on the host machine is mounted into a container
    - does not need to exist on the Docker host already
    - created on demand if it does not yet exist
- Can't use Docker CLI commands to directly manage bind mounts
- Limited functionally compared to volumes
    - When you use a bind mount, a file or directory on the host machine is mounted into a container
    - The file or directory is referenced by its full or relative path on the host machine
- Bind mounts allow access to sensitive files
    - You can change the host filesystem via processes running in a container

### tmpfs mounts
tmpfs mounts are stored in the host system's memory only, and are never written to the host system's filesystem.
- Stored in the host system's memory only
    - never written to the host system's filesystem
- When the container stops, the tmpfs mount is removed, and files written there won't be persisted
- Unlike volumes and bind mounts
    - a tmpfs mount is temporary, and only persisted in the host memory
    - you can't share tmpfs mounts between containers.
<br>
### Create volume
docker volume --help
docker volume create myvol-1
docker volume ls
### Inspect created volume
docker volume inspect myvol-1

### Install Jenkins
docker pull jenkins/jenkins:2.277.4

### Execute Jenkins with Volume
docker run -p 8080:8080 -p 50000:50000 -v myvol-1:/var/jenkins_home jenkins/jenkins:2.277.4