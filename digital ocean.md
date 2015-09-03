# Digital Ocean

Use [mup](https://github.com/arunoda/meteor-up)

## Setup
1. http://stackoverflow.com/questions/13444105/how-to-deploy-a-rails-app-to-a-vps-or-dedicated-server/13444106#13444106
2. See below

```shell
sudo addduser USER # then fill info
sudo adduser USER sudo # add to sudo group

# (optional) add to ssh 
# http://askubuntu.com/questions/16650/create-a-new-ssh-user-on-ubuntu-server
sudo vi /etc/ssh/sshd_config
  # insert AllowUsers USER, then wq
  
# change editor to use vi
sudo update-alternatives --config editor
# edit visudo with vim
# follow the guide on mup readme: NOPASSWD:ALL
# or https://www.digitalocean.com/community/articles/how-to-edit-the-sudoers-file-on-ubuntu-and-centos
```

If you want nginx support:
- [mup doc](https://github.com/arunoda/meteor-up/wiki/Using-Meteor-Up-with-NginX-vhosts)
- [digital ocean guide](https://www.digitalocean.com/community/tutorials/how-to-set-up-nginx-server-blocks-virtual-hosts-on-ubuntu-14-04-lts)

More security setup from this [linux workstation checklist](https://github.com/lfit/itpol/blob/master/linux-workstation-security.md):
- [Make sure root mail is forwarded to an account you check](https://github.com/lfit/itpol/blob/master/linux-workstation-security.md#root-mail)


## MongoDB

Script to backup:

```bash
#!/bin/bash
 
MONGO_DATABASE="USE_YOUR_APP_NAME"
APP_NAME="USE_YOUR_APP_NAME"

MONGO_HOST="127.0.0.1"
MONGO_PORT="27017"
TIMESTAMP=`date +%F-%H%M`
MONGODUMP_PATH="/usr/local/bin/mongodump"
BACKUPS_DIR="./backups/$APP_NAME"
BACKUP_NAME="$APP_NAME-$TIMESTAMP"
 
# mongo admin --eval "printjson(db.fsyncLock())"
# $MONGODUMP_PATH -h $MONGO_HOST:$MONGO_PORT -d $MONGO_DATABASE
$MONGODUMP_PATH -d $MONGO_DATABASE
# mongo admin --eval "printjson(db.fsyncUnlock())"
 
mkdir -p $BACKUPS_DIR
mv dump $BACKUP_NAME
tar -zcvf $BACKUPS_DIR/$BACKUP_NAME.tgz $BACKUP_NAME
rm -rf $BACKUP_NAME

```

crontab:

```
# run every day at 12am
00 00 * * * path/backup_mongodb.sh

```


[How to manually backup or restore](http://stackoverflow.com/questions/11024888/is-there-a-simple-way-to-export-the-data-from-a-meteor-deployed-app/16380978#16380978):
```
mongodump -d dbname 
#or 
mongodump --port 3001 --username meteor mongorestore --port 3001
```