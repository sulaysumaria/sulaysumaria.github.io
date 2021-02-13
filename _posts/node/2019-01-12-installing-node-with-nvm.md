---
layout: post
title: 'Installing Node with NVM'
categories: [Node]
permalink: /installing-node-with-nvm
---

`nvm` is the best tool to install node on UNIX. It has some of the features that makes it very helpful to developers working on multiple projects that require different node versions.

`nvm` allows you to switch node versions instantly. Installing node versions is also just a command.

To install `nvm`, run following command from your home directory:

```bash
# install nvm
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.37.2/install.sh | bash
```

After installing nvm, install node using following:

```bash
nvm install node
```

This will install latest node version available to nvm.

Some usefull commands:

- `nvm ls`
  Lists all the versions of node installed.
- `nvm ls-remote`
  Lists all the versions of node available.
- `nvm install v14.15.5`
  Install specific version of node.
- `nvm use v14.15.5`
  Use specific version of node.

Updating to a newer version of node:

```bash
nvm ls-remote
nvm install v14.15.5
nvm uninstall v14.15.5
```
