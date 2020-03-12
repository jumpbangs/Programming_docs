# DevOps

A pocket or a reference file that can be used for devops. The following is a work in progress file and it will be updated time to time.

## Contents

1. Working with Linux
2. Docker
3. CI/CD
4. Alternative System


## 1. Working with Linux

Linux is an open source and community-developed Operating System(OS) for computer, servers, mainframes, mobile devices and embedded systems. There are many different versions of Linux which is also referred to as distributions(distro) which is used for each specific system. Such popular distributions that is being used are Ubuntu/Red hat for servers and for personal usage are Ubuntu, Arch and Debian. 

### 1.1 Linux Directory Structure

Linux directory is based on file system hierarchy standard, which is a standard that is used by Unix distribution developers, package developers and system implementations. These files can be accessed by using the forward slashes (/) to gain deeper access into other files. The following table lists out the descriptor of each file location.

| Directory | Description                                                                                                      |
|-----------|------------------------------------------------------------------------------------------------------------------|
| /(root)   | The root file system is top-level directory that contains files that is required to boot Linux system            |
| /bin      | The following directory contains user executable files                                                           |
| /boot     | Contains static bootloader and kernel executable and configuration files                                         |
| /dev      | Contains device files for every attached devices to the system.                                                  |
| /etc      | Contains local system configuration for host computer                                                            |
| /home     | Home directory storage for user, each user has their own subdirectory in /home                                   |
| /media    | A place where external removable media are connected                                                             |
| /opt      | Optional files where vendor supplied applications programs are located.                                          |
| /tmp      | Temporary directory that used by the system and programs, users can also store files here temporary.             |
| /use      | Contains shareable, read-only files, executable binaries and libraries.                                          |
| /var      | Contains variable data files such as log files, MY SQL and other database, web server data files, email inboxes. |



### 1.2 Linux Command

The following are command that is used in Linux for daily usages in the Linux terminal. These command will be handy not only in the usage of terminal but in usage of script to execute these commands.

#### 1.2.1 File Command

The list shows Linux file commands that is use on a regular basis when using a Linux terminal.
```
 - pwd : Shows the path file of the current directory
 - cd <dir>  : Change directory to the current or previous
 - ls 	: List out all the files in the current directory 
 - cat <file> : Displays the file content
 - tail <file> : Displays the last five lines of the file
 - head <file> : Displays the first five lines of the file

```
 
The following list shows how to move/copy files to the desired folder or directory.

```
 - ~ : Home directory of the user
 - . : Current directory of the file
 - cp <file> <newFile> : Copy the file with the given file name
 - cp <dir/file> <dir/newFile> : Copy the file with the given file name from the
   given directroy to the other directory
 - mv <dir/file> <dir/newFile> : Moves the file with the given file name to to given
   directory   
 ```

The following list shows how to change the file permission, that is commonly
used.This [calculator](https://chmod-calculator.com/) helps you list out the
custom file permission.
| Value | Meaning                                       |
|-------|-----------------------------------------------|
| 600   | Only the owner has read and write permission. |
| 644   | Only the owner has read and write permissions; the group and others
have read only permission.|
| 700 | Only the owner has read, write and execute permission. |
| 755 | The owner has all permission; the group and others have only read and
execute permission.|
| 711 | The owner has all permissions; the group and others have only execute
permission.|
| 666 | Everyone can read and write to the file.:warning: |
| 777 | Everyone can read, write and execute. :warning:   |

Use the following command to apply this changes to all the files in the
following directory.
```
 - chmod -R <file permission> <file/dir> 
```

To list out the permissions the following line displays the file permissions. In
both settings and numerical value.
```
 - ls -al <dir> : Displays the file permission in setttings value.
 - stat -c "%a %n" * : Displays the file permission in numberical value.
```
#### 1.2.2 Install/Remove of Pacakges

The following are commands that is commonly used to install and remove packages
that the user requires in the system. As the package manager varies from distros
as Debain-based distro uses __APT__, RPM-based distro uses __YUM__ and
Pacman-based distro uses __pacman__. However as most server are based on either
Debain or RPM so the following examples are only in __APT__ and __YUM__.

#### APT commands

+ To update and Install updates
```
 - apt-get update : gets update the installed packages
 - apt-get upgrade : installs the updates of installed packages
```
+ To install and uninstall packages/programs
```
 - apt-get install <package name> / dpkg -i <package name> : installs package
 - apt-get --purge remove <package name> : removes the installed package and
   configuration/settings files
 - dpkg -r <package name> : removes the installed package only
 - dpkg -P <package name> : removes the configuration/settings files of the
   package
```
+ To list out all or find a package/program
```
 - dpkg -l
 - dpkg -l | grep <package name>
```

#### RPM commands

+ To update and Install updates
```
 - yum check-update
 - yum upgrade
 - yum update <package name> : Updates a specific package
```
+ To install and uninstall packages/programs
```
 - yum install <package name>
 - yum remove/erase <package name>
 - yum reinstall <package name> : reinstalls the package again
```

+ To list out all or find a package/program
```
 - yum list installed
 - yum list installed <package name>
```

#### 1.2.3 Finding and Killing a Process
Sometimes a program/software will become unresponsive, which has to killed or
terminated forcefully. This could be difficult if there is no graphical user
interface however in linux it is possbile to terminate a process via command
line. The following examples will show how to do so.

+ To show all process that is running currently.
```
 - ps aus
```

+ To find process by name
```
 - ps aux | grep '<process name>'
```

+ To get the Process ID(PID) of the process
```
 - pidof <program name>
```

+ To kill the process 
```
 - kill -9 <process name/ process id>
```
+ The following is a Task Manager version in terminal
```
 - top
 - htop
```

#### 1.2.4 Creating/Adding Linux Users

The following command will create/add a new user with a password prompt when
creating the user. It will create a user home directory and other setttings
which is a less hassle way to creating a new user. 
```
 - adduser <username>
```

The following command does the same but it will only create the user, hence
adding password to the user is done with another command given below.
```
 - useradd <username> : creates a new user
 - passwd <username> : sets password to the current user
```

The following command creates a user and adds to a exisiting directory.
```
 - useradd -d <dir> <username>
```

The following command adds the user to a Group, this is useful as by adding a
user to a group it grants the user permissions to read, write and execute files.
```
 - useradd -G <group name> <username>
```
 
### 1.3 Webserver
As most webservers are using linux based distro, which are running apache or
nginx the common web host servers. There different servers such as nodejs and
flask but apache and nginx are the two most popluar webservers used to host
websites or API backend server. 

This section will show how to install and setup both apache and nginx
servers. It will go over how to intall and setup MySql database and installing
Php to use phpmyadmin a database interface.

#### 1.3.1 Installing Apache/Nginx

The following are step by step commands to install apache/nginx in a linux based
system.

#### Installing Apache

```
1. sudo apt-get update
2. sudo apt-get install apache2
```
To check if the apache has be successfully installed, click on the following
link to check [localhost](http://localhost). It should show up the default
apache page.


