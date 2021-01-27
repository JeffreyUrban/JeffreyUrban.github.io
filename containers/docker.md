---
title: Docker
parent: Containers
---

# Install on Ubuntu:  
[Reference](https://docs.docker.com/install/linux/docker-ce/ubuntu/)  

_don't create docker group, instead require root/sudo_  

```
sudo apt update  
sudo apt-get install apt-transport-https ca-certificates curl gnupg-agent software-properties-common  
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -  
sudo apt-key fingerprint 0EBFCD88  
sudo add-apt-repository "deb arch=amd64 https://download.docker.com/linux/ubuntu \  
    $(lsb_release -cs) \  
    stable"  
sudo apt update  
sudo apt install docker-ce docker-ce-cli containerd.io  
sudo docker run hello-world  
sudo systemctl enable docker  
```

# Build image:  

`sudo docker build`   

# List images:  

`sudo docker image ls`  

# Remove image:  

`sudo docker image rm`   

# Remove all stopped containers, inactive networks, dangling images and build cache:  

`sudo docker system prune`  

# Docker on edge - look into Foghorn  

[https://www.foghorn.io/](https://www.foghorn.io/)  

# Determine ownership of container and volume overlay2s:

{% raw %}
`docker inspect -f $'{{.Name}}\t{{.GraphDriver.Data.MergedDir}}' $(docker ps -aq)`
{% endraw %}

# Move docker cache

`/lib/systemd/system/docker.service`:

`ExecStart=/usr/bin/dockerd -g <desired-cache-path> -H fd:// --containerd=/run/containerd/containerd.sock`

_This may break some privileged workflows, such as losetup_

# Clean up docker cached images

[Reference](https://lebkowski.name/docker-volumes/)

```
docker images --no-trunc | grep '<none>' | awk '{ print $3 }' \
    | xargs -r docker rmi
```

To include named containers and dependencies

`docker image ls -a | awk '{ print $3 }' | xargs -r docker rmi`
