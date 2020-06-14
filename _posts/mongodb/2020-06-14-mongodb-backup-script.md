---
layout: post
title: "MongoDB Backup Script"
categories: [MongoDB]
permalink: /mongodb-backup-script
---

If you have your MongoDB setup on a server, then it is always good to have a system setup that backups database every day and keeps it somewhere safe. So that, you can recover your database in case of data being lost or if you want to time travel in past.

Here is a script that takes backup of your database and saves it as tar.gz

```bash
#!/bin/sh
DIR=myApp_production-`date +%y%m%d_%H%M%S`
DEST=/root/db_backups/$DIR
mkdir $DEST
mongodump --db myApp_production -o $DEST -u <username> -p <password> --port <port> --forceTableScan
tar czf $DIR.tar.gz $DEST
```

To take backup every day, setup following in the crontab. You can set the cron time to suite your usecase.

```bash
crontab -e
# Add below line to crontab
45 1 * * * /root/backup_scripts/backup_myApp_production.sh
```
