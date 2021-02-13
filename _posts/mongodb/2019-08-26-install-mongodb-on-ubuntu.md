---
layout: post
title: 'Installing MongoDB on Ubuntu'
categories: [MongoDB]
permalink: /install-mongodb-on-ubuntu
---

Today I faced a similar issue on linux server. MongoDB on linux server was 3.x while what I was using for development 4.x. Everything was going well until today, I used a feature that was introduced in MongoDB in 4.0 and it broke the staging environment. Maybe that's why we have staging environment, so that things can break before going to production.

The solution I decided to go with was to completely uninstall 3.x and install 4.x on server. Of course it meant a little down time, but updating database is a must. Uninstalling MongoDB can be easy, but installing it can be tricky sometimes. You can successfully install it, but registering it as a service can be more tricky. So here are some commands that can help you with uninstalling/installing MongoDB.

## Backup database

Though this process will not affect your database, but it is always good to keep a backup of your databases before doing such critical tasks. Also make sure to backup your database before uninstalling MongoDB.

Suppose your database name is `counter`. To backup your database(s) you can use `mongodump`:

```bash
cd ~
mongodump --db counter
```

This will create a `dump` directory and inside it a `counter` directory.

## Uninstalling

Run the following commands to remove MongoDB:

```bash
sudo apt purge mongodb mongodb-clients mongodb-server mongodb-dev
sudo apt purge mongodb-10gen
sudo apt autoremove
```

## Installing

Before installing, make sure to remove old ppas. Head over to `/etc/apt/` and scan each file for traces of MongoDB and remove them if any.

Next run following commands:

```bash
wget -qO - https://www.mongodb.org/static/pgp/server-4.4.asc | sudo apt-key add -
echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu bionic/mongodb-org/4.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.4.list
sudo apt-get update
sudo apt-get install -y mongodb-org
```

To check if MongoDB is installed correctly, run `mongod` and it should say `Waiting for connections on port 27017`. Hit `Ctrl + C` to exit. We will be using MongoDB service, instead of keeping a terminal session open. To start MongoDB as a service run following command:

```bash
sudo service mongod start
```

To check if service is started, run `mongo` and see if it connects to database. If yes, you are ready to go. If no, follow below steps.

## Setting up MongoDB service

Create a new service file

```bash
nano /lib/systemd/system/mongodb.service
```

Copy following text to that file:

```
[Unit]
Description=MongoDB Database Server
Documentation=https://docs.mongodb.org/manual
After=network.target

[Service]
User=mongodb
Group=mongodb
EnvironmentFile=-/etc/default/mongod
ExecStart=/usr/bin/mongod --config /etc/mongod.conf
PIDFile=/var/run/mongodb/mongod.pid
LimitFSIZE=infinity
LimitCPU=infinity
LimitAS=infinity
LimitNOFILE=64000
LimitNPROC=64000
LimitMEMLOCK=infinity
TasksMax=infinity
TasksAccounting=false
Restart=always

# Recommended limits for for mongod as specified in
# http://docs.mongodb.org/manual/reference/ulimit/#recommended-settings

[Install]
WantedBy=multi-user.target
```

Now run following to setup the service:

```bash
sudo systemctl enable mongodb.service
```

To start and stop your service, you can use following commands:

```bash
sudo systemctl start mongodb
sudo systemctl stop mongodb
```

## Restore Database

After you have successfully setup MongoDB, time to restore your database. Refer to following commands to restore database:

```bash
cd ~/dump/counter
mongorestore --db counter .
```
