# Linux up skill Challenge

1. Day 0 - Creating your own Server ( Digital Ocean plan)
2. Day 1 - Accessing server and changing password
3. Day 2 - Basic Navigation 
4. Day 3 - Power Trip
5. Day 4 - Installing/removing Program  and usage of Midnight commander.

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

## Day 3

###### Power Trip

The command `sudo` is used to execute a command : `sudo apt update` with elevated privileges (usually as root). It can enable a non-root user to execute the same command with root privileges but he/she must be granted access to the `sudo` command.

To add a non-root user to allow run `sudo`, you can run the following command :  `sudo adduser <username> sudo` in the terminal to grant him/her the access of running `sudo`. However if you would like to execute a several root commands in a non-root user account, you can run the following command: `sudo -i`  to access root privileges  .

The following command : `sudo !!` re-runs the last/previous command as root.

As stated in Day 3, the command `ls -l` will print out the permissions for file/folder. If the following file/folder has only root access, any of these command: `cat`,`less`, `nano` and `head` will not work unless they are paired with `sudo`. 

The following file `/etc/shadow` holds the hashed passwords for the server in which is the prime target for intruders and the following file `/var/log/auth.log` holds the logs of what commands were executed by which users that were/are in the system. To filter out the logs you can use the `grep` command to do so, for example `grep "sudo"/var/log/auth.log` will filter out any logs that has the word `sudo` that is being used.

###### Renaming server name and setting time

To rename your server, edit both of the following files `/etc/hostname` & `/etc/hosts`  using the command line editor of your choice in my case I prefer using **vim**. Hence to edit the following file this would be my command : `sudo vim /etc/hostname` & `sudo vim /etc/hosts` which i replace the old name with the new name of my choice. To apply changes you will need to reboot you system in which you would have to run the following command : `sudo reboot`.

To change timezone in your server run the following commands:

1. To check your current time setting:

   `timedatectl`

2. Get the list of available timezones:

   `timedatectl list-timezones`

3. To set the timezone just run :

   `sudo timedatectlset-timezone Asia/Kathmandu`

4.  To confirm again:

   `timedatectl`

## Day 4

###### Installing Software, exploring the file structure

To search for applications in the `apt` repository just use the following command: `apt search "your_application"`; example `apt search "midnight commander"`. This would list out the range of packages that are available in the repository and you can install the desired application via the following command: `sudo apt install "your_application"`; example to install **midnight commander** just input `sudo apt install mc` this would install the following package/program.

It would prompt you for the password and double confirm to install the following package/program. You can use the following command :`sudo apt install mc -y` this would let you skip the prompt if you want to install the program/package.

###### Midnight Commander 

**Midnight commander** is an terminal based file explorer, in would viewing files from the terminal more easily, furthermore you can use the mouse to select the files/options. To know more on how to use the following application just use the following command: `man mc`.

***Basics commands for MC***

1. Press `F3` to view the file and  again  to exit the file/folder.
2. Press `F4`to edit your file using the given text editor by MC.
3. Press `F5` to copy the file/folder to the desired folder destination (you're required to fill in the full directory path).
4. Press `F6` to rename/move the file/folder to the desired name/directory.
5. Press `F7 ` to create a folder.
6. Press `F8` to delete folder/file.
7. Press `F9` for more options.
8. Press `F10` to quit MC.

###### Removing/uninstalling  packages/program

To remove programs/packages you can use the following command : `sudo apt remove "your_application"` or to completely remove the package/program plus it's dependences the following command: `sudo apt remove --purge "your_application"`. 

