---
layout: post
title: "Installing Docker on Ubuntu"
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
sudo curl -L "https://github.com/docker/compose/releases/download/1.24.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
docker-compose --version
```
