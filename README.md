## WIP note
This is a work in progress. After starting the practice of mounting sda2 as my root drive (a thumb drive) and only using the SD card for /boot, I found that the corruption rate for my pis fell to literally zero.

That said, this is still a handy few roles and as I get more local infrastructure I should be able to flesh this out more.

# generic-pi
Provision a generic raspberry pi running raspbian. Provisioning refers to the act of taking a stock system and making it ready to do the work it is intended to do.

In my case, it means set up a user and trash the pi user, set up a new hostname, install some bits like fail2ban and docker, and mount /var/log as a ramdisk to further avoid filesystem corruption due to unexpected power failures.

# Usage
Create a vars/common.yaml file with your username and hostname you'd like to set. Then make sure you can ssh into your pi- please manually change your pi's password to something very strong (read: very very long) before you connect it to a network, and as this script will remove password authentication for ssh, please set up your ssh key with the pi before you start:

```
ssh-copy-id pi@192.168.1.12
```

To provision your pi:
```
ansible-playbook -i inventory.yaml ./pi.playbook.yaml all
```

## What's it do
The usual bunch of things. Specifically:

* adds hypriot's docker-for-pi to the system
* Updates hostname to specified hostname in vars/common.yaml
* secures ssh and adds fail2ban
* Adds a new user with passwdless sudo and docker access
* updates logs to write to tmpfs directory

## 
