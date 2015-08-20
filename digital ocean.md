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