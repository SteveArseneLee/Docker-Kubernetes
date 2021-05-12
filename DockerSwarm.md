## Swarms
### Without Hyper-V
docker-machine create default --virtualbox-no-vtx-check
### Create a VM
docker-machine create --driver virtualbox myvm1
### Win10
docker-machine create -d hyperv --hyperv-virtual-switch "myswitch" myvm1
### View basic information about your node
docker-machine env myvm1
### List the nodes in your swarm
docker-machine ssh myvm1 "docker node ls"
### Inspect a node
docker-machine ssh myvm1 "docker node inspect <node ID>"
### View join token
docker-machine ssh myvm1 "docker swarm join-token -q worker"
### Open an SSH session with the VM; type "exit" to end
docker-machine ssh myvm1
### View nodes in swarm (while logged on to manager)
docker node ls
### Make the worker leave the swarm
docker-machine ssh myvm2 "docker swarm leave"
### Make master leave, kill swarm
docker-machine ssh myvm1 "docker swarm leave -f"
### list VMs, asterisk shows which VM this shell is talking to
docker-machine ls
### Start a VM that is currently not running
docker-machine start myvm1
### show environment variables and command for myvm1
docker-machine env myvm1
### Mac command to connect shell to myvm1
