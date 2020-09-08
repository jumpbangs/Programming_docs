# Linux up skill Challenge

1. Day 0 - Creating your own Server ( Digital Ocean plan)

## Day 0

#### Signing Up

Create a droplet plan by following through the start-up plan but select $5/month plan droplet. Follow through the installation/set-up plan for the following droplet.

#### Logging in for the first time

To access your droplet for the first time, you can access it via using the following command:

`ssh root@ipaddress_that_is_given_to_you`

the password would be the one that you have created at the start of creating/setting-up a droplet .

#### Creating a working administrator account

To avoid logging in as root to the main account or accessing the main account via ssh, it would be a good approach would be to create a user with root access. In which is done via the following steps:

```
1. adduser `username`
2. usermod -a -G adm `username`
3. usermod -a -G sudo `username`
```

The following `adm` group allows the user to read log files, xconsole and sudo for access as root/admin user. Run the following command to fetch and install updates on the system which is `sudo apt update ` and `sudo apt upgrade`, the following command will fetch any updates and then apply those fetched updates.

#### Disabling the root user

You can run the following command `sudo usermod -p "!" root` to disable the access for root user via ssh, however be warned the following command makes root login impossible. If there is a need to login in as root, use the following command `sudo passwd -l root`, this will lock the user and it can be unlocked in the later future.

## Day 1

#### Logging into your account

To login to your droplet/server account just run the following command: `ssh 'username'@<ip_address>`, which is for example  `ssh newuser@192.168.213.15`.  In which will prompt you for a password that you had created for a new user. 

To create a password-less ssh login follow the these steps to do so :

1. Check for existing SSH key pair, just run the following command :

   `ls -al ~/.ssh/id_*.pub`

   If the following command gives an output of `No such file or directory` or `no matches found`, there is no existing ssh key files. If there is you can skip the following steps. 

2.  To generate a new SSH key pair run the following command : 
   `ssh-keygen -t rase -b 4096 -C 'your_email@domain.com'`
   
   Press `Enter` to accept the default file location and file name. It will prompt you to type a secure pass-phrase for an extra layer of security but you can skip it as it optional.  Once that is done, your SSH keys would be generated and just run the following command to check if they are generated :

   `ls ~/.ssh/id_*`

3.  Copy the public key

   To copy the new/old ssh to your server ( this will allow password-less access to your server ), you can run the following command :

   `ssh-copy-id 'your_remote_username'@<server_ip_address>` for example : `ssh-copy-id newuser@192.168.213.15` 

   The following command will prompt you for your server's password for that following user, just enter the correct password and if everything goes well you will be logged in your server account with a password prompt. However is the following command `ssh-copy-id` is not found you can run the following command to do the same execution :

   `cat ~/.ssh/id_rsa.pub | ssh 'your_remote_username'@<server_ip_address> "mkdir -p ~/.ssh && chmod 700 ~/.ssh && cat >> ~/.ssh/authorized_keys && chmod 600 ~/.ssh/authorized_keys"` 

You can try the following commands : `ls`, `uptime`, `free`, `df -h`, `uname -a`

To change your current user password, you can run the following command : `passwd`, it will prompt you for your old password and then the new password that you would like to you in the future.

## Day 2

#### Basic Navigation

Understanding how to `cd`( change directory or folder location ), using `ls` to list the content of the directories and using `mkdir` to create a new directory in the current directory.

1. `pwd` ( print working directory ) will print out the "location" of the current directory that you are working on
2. `cd` or `chdir` will  move to different directory example `cd /var/log` will direct you to the following directory `/var/log` or you can `pwd ` to check which directory that you are currently on after running the following command : `cd /var/log` 
3.  To move up a directory just type `cd ..` or to move straight back to the home directory just type `cd` . By entering `cd ..` you will move from `/directory1/directory2`to `/directory1` if you were at `directory2 ` in the beginning.
4.  To check what is in the current directory just use the following command : `ls` this would list out all the files/contents that is in the current directory. However to list all the files/contents in the current including the hidden ones run the following command: `ls -a` this will list out all the hidden files such as `.hiddenfile` in the directory. 
5. To sort out the files according to the date that they were recently modified just run : `ls -t` this will list out the files/contents that sorted out by which was recently modified to the  last modified. To reverse the following sorting method just run : `ls -tr` 
6. To list out the file's permissions just use the following command : `ls -l` this would list out each file/contents permissions.
7. To create a new directory in the current directory just run `mkdir test`, this would create a directory called `test` in the current folder.
8.  If you are unsure or what to know what command does or more features of the command just run the following command : `man ls` , `man pwd`, `man cp` these will show the full details and functionality of each commands ( this is a manual page for each commands).

