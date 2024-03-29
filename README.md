# CPSC4810-HackPack
## 30 Minute Check List
* Change the root password.
	* $ `passwd root`
* Check /etc/passwd to see users. 
	* $ `cat /etc/passwd`
* Change passwords of other users with login.
	* $ `passwd username`
* Delete unneeded users
	* $ `userdel username`
* Check /etc/group and /etc/shadow.
	* $ `cat /etc/group and cat /etc/shadow`
* Check what's in the crontab and edit it.
	* $ `crontab -l`
	* $ `crontab -e`
* Check /tmp for suspicious files.
	* $ `ls -la /tmp`
* Check people with sudo permission. Do not let users have ALL = (ALL) ALL.
	* $ `visudo`
* Check running processes.
	* $ `ps aux`
	* $ `top`
* Check running services.
	* $ `ss -tulpn`
* Make bakeup of services
	* $ `mkdir backup`
	* $ `sudo mv -v /etc/service.conf /backup/service.conf.bk`
* Update and upgrade
	* $ `yum -y update`
	* $ `reboot`
* Continually check for users on machine
	* $ `who`
## Services
If you edit config files do not forget to restart the service 
### VSFTPd
#### Installation
* $ `sudo apt-get install vsftpd`
* Restart, start, or stop vsftpd
	* /etc/init.d/vsftpd [restart | stop | start]
#### Config File
* Location is /etc/vsftpd.conf 
* Back up config file
	* $ `sudo cp /etc/vsftpd.conf /backup/vsftpd.conf.bk`
* Disable anon users, allow local users, allow users to upload files
	* anonymous_enaable=NO
	* local_enable=YES
	* write_enable=YES
* Limit ftp users to directory.
	* userlist_enable=YES
	* userlist_file=/etc/vsftpd/user_list
	* userlist_deny=NO (Setting this to yes makes user_list a list of blocked users)
* Add following to config file to reduce ftp privileges
	* nopriv_user=ftp
### OpenSSH
#### Installation
* sudo apt-get install openssh-server openssh-client
* Restart, start, or stop ssh
	* `/etc/init.d/ssh [restart | stop | start]`
#### Config File
* Config Location /etc/ssh/sshd_config
* Back up config file
	* $ `sudo cp  /etc/ssh/sshd_config /backup/sshd_config.bk`
* Deny root login
	* /etc/ssh/sshd_config
	* PermitRootLogin no
* Limit user login
	* /etc/ssh/sshd_config
	* AllowUsers (username)
* User public/private keys for auth
	* put pubkey in ~/.ssh/authorized_keys
	* PasswordAuthentication no
#### Kicking an active user off
* Find process ID using `ps -a | grep ssh`
* `kill [pid]`
### Apache
#### Installation
* sudo apt-get install apache2
* Restart, start, or stop apache2
	* `/etc/init.d/apache2 [restart | stop | start]`
#### Config File
* Configuration file is found in /etc/apache2/apache2.conf
* Back up config file
	* $ `sudo cp /etc/apache2/apache2.conf /backup/apache2.conf.bk`
* Add "ServerTokens Prod" to remove version information
* Add "ServerSignature Off" to change header
* To restric directory browsing
	*/etc/apache2/apache2.conf
 ``` 
<Directory />
Order Deny,Allow
Deny from all
Options None
AllowOverride None
</Directory> 
```
#### Backup Server
* $ `sudo cp /var/www/ /backup/var`

### MySQL
#### Installation
* sudo apt-get install mysql-server
* sudo mysql_secure_installation
* Restart, start, or stop mysql
	* $ `/etc/init.d/mysql [restart | stop | start]`

#### Reset MySQL Root Password
* sudo /etc/init.d/mysql stop
* sudo /usr/sbin/mysqld --skip-grant-tables --skip-networking &
* mysql -u root
* FLUSH PRIVLEGES
* SET PASSWORD FOR root@'localhost' = PASSWORD('password');
* UPDATE mysql.user SET Password=PASSWORD('newpwd') WHERE User='root';

#### Create backup of MySQL Database
* $ `mysqldump -u USER -p --all-databases > /backup/all_databases.sql`

### AD/DS

## WINDOWS
* Add user: `net user <username> <password> /ADD`
* Change password: `net user <username> *`
* See who is logged on: `query user`, use `logoff <ID>` to kick them off
* Disable an account: `net user <username> /active:no`
* Check services: `services.msc`
* Users and Groups: `lusrmgr.msc`
* Security Policies: `secpol.msc`
* Add network rule: `netsh advfirewall add rule=”<name>” dir=[in | out] action=allow protocol=[TCP | UDP] localport=<port>`
* Look at listening/open ports: `netstat -an`


## Extras
* Check for shells
	* $ `grep exec * -R`
* Check File attribute
	* $ `lsattr filename`
* Change File Attribute
	* $ `chattr [+/-/=] [attribute] filename`

