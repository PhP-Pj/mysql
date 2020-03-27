# mysql
Install
https://phoenixnap.com/kb/how-to-install-mysql-on-ubuntu-18-04 Problem with signature.  
Opting for https://linuxize.com/post/how-to-install-mysql-on-ubuntu-18-04/
an earlier version   (5.7)

### Root
mysql -u root -p or  
sudo mysql

### Admin
admin mypswd_DB!

### Admin comnands
see https://linuxize.com/post/how-to-manage-mysql-databases-and-users-from-the-command-line/ to  
* create DB
* create users
* privileges
* ...

update mysql.user set Grant_priv='Y' where host='localhost' and user='admin';

### Creating a DB
mysql -u admin -p
```
mysql> CREATE DATABASE phpdb;
```
#### Creating user
```
mysql> CREATE USER 'php_user'@'localhost' IDENTIFIED BY 'the password';
```

#### Grant privileges
GRANT ALL PRIVILEGES ON database_name.* TO 'database_user'@'localhost';  
or  
GRANT SELECT, INSERT, DELETE ON database_name.* TO database_user@'localhost';  
FLUSH PRIVILEGES;  

## PhpMyAdmin

See:
* https://linuxize.com/post/how-to-install-and-secure-phpmyadmin-with-apache-on-ubuntu-18-04/
* https://hostadvice.com/how-to/how-to-install-apache-mysql-php-on-an-ubuntu-18-04-vps/  

UI used to adminstrate mysql.  
It runs on apache2 so the php module for apache needs to be installed:
```
sudo apt-get install php libapache2-mod-php
```

But I add to follow https://askubuntu.com/questions/387062/how-to-solve-the-phpmyadmin-not-found-issue-after-upgrading-php-and-apache to add the phpmyadmin site

TL;DR;
```
sudo ln -s /usr/share/phpmyadmin /var/www/html
sudo ln -s /etc/phpmyadmin/apache.conf /etc/apache2/conf-available/phpmyadmin.conf
sudo a2enconf phpmyadmin.conf
sudo service apache2 reload


```


### Admin User
phpmyadmin  
..._DB!  
To grant it all the rights I used user/paswword found in /etc/mysql/debian.cnf (debian-sys-maint)

### User lambda
It seems like for **phpmyadmin** to create a user it needs to select **Authentication Plugin** **Unix socket based auth**
