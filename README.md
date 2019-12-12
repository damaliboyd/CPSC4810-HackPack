# CPSC4810-HackPack
## 30 Minute Check List
* Change the root password.
	* $ passwd root
* Check /etc/passwd to see users. 
	* $ cat /etc/passwd
* Change passwords of other users with login.
	* $ passwd username
* Delete unneeded users
	* $ userdel usernmae
* Check /etc/group and /etc/shadow.
	* $ cat /etc/group and cat /etc/shadow
* Check what's in the crontab and edit it.
	* $ crontab -l
	* $ crontab -e
* Check /tmp for suspicious files.
	* $ ls -la /tmp
* Check people with sudo permission. Do not let users have ALL = (ALL) ALL.
	* $ visudo
* Check running processes.
	* $ ps aux
	* $ top
* Check running services.
	* $ ss -tulpn
* Update and upgrade
	* yum -y update
	* reboot
* Continually check for users on machine
	* who
## Services
### pfSense
### VSFTPd
#### Installation
* sudo apt-get install vsftpd.
####
* /etc/vsftpd.conf 
### OpenSSH
#### Installation
* sudo apt-get install openssh-server openssh-client

#### Config File
* etc/ssh/sshd_config
* Deny root login
	* etc/ssh/sshd_config
	* PermitRootLogin no
* Limit user login
	* /etc/ssh/sshd_config
	* AllowUsers (username)
* User public/private keys for auth
	* put pubkey in ~/.ssh/authorized_keys
	* PasswordAuthentication no

### Apache
* Configuration file is found in /etc/apache2/apache2.conf
* Add "ServerTokens Prod" to remove version information
* Add "ServerSignature Off" to change header
* Restart, start, or stop apache2
	* /etc/init.d/apache2 [restart | stop | start]
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
### MySQL and MongoDB
#### Installation
* sudo apt-get install mysql-server
* sudo mysql_secure_installation

#### Reset MySQL Root Password
* sudo /etc/init.d/mysql stop
* sudo /usr/sbin/mysqld --skip-grant-tables --skip-networking &
* mysql -u root
* FLUSH PRIVLEGES
* SET PASSWORD FOR root@'localhost' = PASSWORD('password');
* UPDATE mysql.user SET Password=PASSWORD('newpwd') WHERE User='root';

#### Create backup of MySQL Database
15 2 * * * root mysqldump -u root -pPASSWORD --all-databases | gzip > /mnt/disk2/database_'data ' %m-%d-%y' ' .sql.gz

### AD/DS

## Extras
Check for shells
```
$ grep exec * -R
```
