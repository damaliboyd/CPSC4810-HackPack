# CPSC4810-HackPack
## 30 Minute Check List
* Check Users and Groups. Remove any unneeded users and change passwords.
* Check configurations of SSH, Web Server
* 
## Extras
Check for shells
```
$ grep exec * -R
```

### pfSense
### VSFTPd

## OpenSSH
* sudo apt-get install openssh-server openssh-client

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
 ### Nginx
 * /etc/nginx/nginx.conf
* Audit the server
  * sudo apt-get install wapiti
	* wapiti http://example.org -n 10 -b
  
## Postfix, Dovecot, and Bind9

## MySQL and MongoDB
#### Installation
* sudo apt-get install mysql-server
* sudo mysql_secure_installation
#### Commands
#### Reset MySQL Root Password
* sudo /etc/init.d/mysql stop
* sudo /usr/sbin/mysqld --skip-grant-tables --skip-networking &
* mysql -u root
* FLUSH PRIVLEGES
* SET PASSWORD FOR root@'localhost' = PASSWORD('password');
* UPDATE mysql.user SET Password=PASSWORD('newpwd') WHERE User='root';

#### Create backup of MySQL Database
15 2 * * * root mysqldump -u root -pPASSWORD --all-databases | gzip > /mnt/disk2/database_'data ' %m-%d-%y' ' .sql.gz

## AD/DS and AD DNS

