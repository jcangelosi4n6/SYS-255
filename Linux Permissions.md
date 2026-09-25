# Linux Permissions
Managing user's and groups on linux is key to eliminating unnecessary privileges creating vulnerabilities.  
We're going to add both to our dhcp01 box to test how these are managed.  
## Creating Users
```
useradd [username]
passwd [username]
ls -ls /home/[username]
```
  * The last command is used to check the permissions on the user's home directory
## Permissions Bits
  * 1st bit is the type of file
    * d for directory etc
  * 2-4 is for the owner
  * 5-7 are for group
  * 8-10 are for other
## Create Groups
```
groupadd [groupname]
usermod -aG [groupname] [username]
```
### Changing group on files and directories
```
chgrp [groupname] [file/dorectory]
chmod [owner/group/other]+[read/write/execute] [file/directory]
```
