---
layout: post
title: 'Installing Docker on Ubuntu'
categories: [Docker]
permalink: /installing-docker-on-ubuntu
---

Here are a list of commands that, if all are executed successfully, will install docker and docker-compose on your linux machine.

```bash
# Installing dependencies
sudo apt update
sudo apt install apt-transport-https ca-certificates curl gnupg-agent software-properties-common

# Installing docker
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt update
sudo apt install docker-ce
sudo systemctl status docker

# Installing docker compose
sudo curl -L "https://github.com/docker/compose/releases/download/1.28.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
docker-compose --version

# Clear docker logs
# Note: Do not copy below line if you are viewing source code, it is modified to
# work with jekyll as jekyll skips the double curly braces as its templating
# Actual commsnd: echo "" > $(docker inspect --format='{{.LogPath}}' <container_name_or_id>)
echo "" > $(docker inspect --format='{{"{{.LogPath"}}}}' <container_name_or_id>)
```

If you want to delete all unused resources that docker created, you can run following command:

```bash
docker system prune --volumes
```
