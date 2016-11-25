# Digital Ocean

Use this [link](https://m.do.co/c/ddb021b2d64b) to register Digital Ocean with $10 credit.

## Setup
- follow https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-14-04
- Follow mup guide:
```
And you also need to add NOPASSWD to your sudoers file. Open it with:

    sudo visudo
    Then, replace the line that says %sudo ALL=(ALL) ALL with

    %sudo ALL=(ALL) NOPASSWD:ALL
```
- Add Public Key to New Remote User, by follow https://gist.github.com/jamiewilson/4e1d28f9a200cb34ad59#set-up-ssl
  - disable root access, change port(using the same guide by editing '/etc/ssh/sshd_config')
    - https://www.digitalocean.com/community/questions/what-is-the-effect-of-permitrootlogin-no
- follow https://www.digitalocean.com/community/tutorials/additional-recommended-steps-for-new-ubuntu-14-04-servers
- add fail2ban by: https://www.digitalocean.com/community/tutorials/how-to-protect-ssh-with-fail2ban-on-ubuntu-14-04
- Don't need to add swap when using SSD

####Optional: 
change editor to use vi `sudo update-alternatives --config editor`

#### References:
- http://julian.io/how-do-i-host-multiple-meteor-apps-on-one-digitalocean-droplet/
- https://gist.github.com/jamiewilson/4e1d28f9a200cb34ad59#add-some-swap-space

#### If you want nginx support:
- [mup doc](https://github.com/arunoda/meteor-up/wiki/Using-Meteor-Up-with-NginX-vhosts) (which automatically use nginx, you don't need to setup anything)
- [digital ocean guide](https://www.digitalocean.com/community/tutorials/how-to-set-up-nginx-server-blocks-virtual-hosts-on-ubuntu-14-04-lts)

More security setup from this [linux workstation checklist](https://github.com/lfit/itpol/blob/master/linux-workstation-security.md):
- [Make sure root mail is forwarded to an account you check](https://github.com/lfit/itpol/blob/master/linux-workstation-security.md#root-mail)

---

## MongoDB

#### automatic backup

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


#### How to manually backup or restore
http://stackoverflow.com/questions/11024888/is-there-a-simple-way-to-export-the-data-from-a-meteor-deployed-app/16380978#16380978
```
mongodump -d dbname 
#or 
mongodump --port 3001 --username meteor 
mongorestore --port 3001 -d meteor FOLDER_THAT_HAS_BSON_FILES
```

#### Oplog
How to enable oplog if the db is already in use?

ref:
- https://github.com/meteor/meteor/wiki/Oplog-Observe-Driver
- (outdated: it's using mongodb 2.4) https://gentlenode.com/journal/meteor-10-set-up-oplog-tailing-on-ubuntu/17
- https://www.digitalocean.com/community/tutorials/how-to-implement-replication-sets-in-mongodb-on-an-ubuntu-vps

---

## SSL

### How to check?
Online tool: https://www.sslshopper.com/ssl-checker.html

Or use `ssl-cert-check` on server ([reference](https://community.letsencrypt.org/t/it-there-a-command-to-show-how-many-days-certificate-you-have/11351/4)):  
```
sudo ssl-cert-check -c /etc/letsencrypt/live/yourdomain.tld/cert.pem
```


### Setup SSL using [mupx](https://github.com/arunoda/meteor-up/tree/mupx) and [Let’s Encrypt](https://letsencrypt.org/)
#### Steps
Make sure A record is already updated for your domain first

SSH to server:

  ```bash
  # ssh to your server
  git clone https://github.com/letsencrypt/letsencrypt
  ./letsencrypt-auto certonly --standalone --agree-tos --email YOUR_EMAIL -d YOURDOMAIN.COM -d www.YOURDOMAIN.COM
  ```
The following 4 files will be generated in the archive folder: `/etc/letsencrypt/archive/YOURDOMAIN.COM`    
(Note the ones in `/etc/letsencrypt/live/YOURDOMAIN.COM` is symlinked to archive folder)
- cert1.pem
- chain1.pem
- fullchain1.pem
- privkey1.pem

  
Now we want to copy those files to your local machine:

  ```
  # compress them on server first
  sudo tar -cvvf letsencrypt_YYYY_MM_DD.tar /etc/letsencrypt/archive/YOURDOMAIN.COM
  # then on your local terminal, use scp to get the above file, copy to home folder
  scp -P 22 USER@IP:/home/USER/letsencrypt_YYYY_MM_DD.tar ~
  # or 
  ```

Put the downloaded two files (fullchain.pem and privkey.pem) in your local folder where mup can access (see mup.json)

Update mup.json

  ```
   “ROOT_URL”: “https://yourdomain.com",
   ...
   "ssl": {
    "certificate": "PATH_TO/fullchain.pem", // this is a bundle of certificates
    "key": "PATH_TO/privkey.pem", // this is the private key of the certificate
    "port": 443 // 443 is the default value and it's the standard HTTPS port
  },
  ```

Don't forget to add `force-ssl` package:  `meteor add force-ssl`

#### Renew automatically
> NOTE this will **NOT** work because the server has to be stopped
> - [ ] maybe try this? https://cuonic.com/posts/automating-lets-encrypt-certificate-renewal

Let’s Encrypt expires 90 days, so we create cron job to automatically update:

  ```
  30 2 * * 1 /home/USER/letsencrypt/letsencrypt-auto renew >> /var/log/le-renew.log
  ```

#### To renew manually
  ```bash
  # on dev machine, stop server:
  mupx stop
  # on server
  /home/USER/letsencrypt/letsencrypt-auto renew
  # above command will generate new files (cert2.pem etc), get the files to local machine
  # by doing the same steps above: 'sudo tar -cvvf ...' (see above)
  mupx setup
  mupx deploy
  ```

Key points:
- You need to stop server before running renew.
- if cert is expired, you need to run `mpux setup` again
- if you run letsencrypt renew, new files will be generated (such as cert2.pem)
  - cert.pem: Your domain's certificate
  - chain.pem: The Let's Encrypt chain certificate
  - fullchain.pem: cert.pem and chain.pem combined
  - privkey.pem: Your certificate's private key


#### Reference: 
- first read this [guide](https://medium.com/@getdrizzle/deploying-meteor-app-with-free-ssl-certificate-mupx-letsencrypt-digital-ocean-7c85d90cc731#.ty1lahoh9
)
- https://www.digitalocean.com/community/tutorials/how-to-secure-nginx-with-let-s-encrypt-on-ubuntu-14-04
- https://forums.meteor.com/t/setting-up-ssl-with-letsencrypt-and-meteorup/14457

Additional:
- [How to create a self-signed SSL Certificate](http://www.akadia.com/services/ssh_test_certificate.html)
