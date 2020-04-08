# mysql and Phpmyadmin

## mysql

### Install
https://phoenixnap.com/kb/how-to-install-mysql-on-ubuntu-18-04 Problem with signature, so I removed the package:  
```
sudo dpkg --remove mysql-apt-config
```

Opting for https://linuxize.com/post/how-to-install-mysql-on-ubuntu-18-04/
an earlier version   (5.7)

### Root
sudo mysql
root uses socket auth so the following command won't work.
mysql -u root -p or  


### Admin
Created an **admin** user (same as root) using native auth so the following command works.
```
mysql -u admin -p
```
admin password root


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

### Issues

#### Timezone

After rebooting I gor this error while trying to open a connection with SQLDEVELOPER:
```
Status : Failure -Test failed: The server time zone value 'CEST' is unrecognized or represents more than one time zone. You must configure either the server or JDBC driver (via the 'serverTimezone' configuration property) to use a more specifc time zone va
```
To fix it I updated the mysql timezone tables in mysql databes with this script
* TABLE time_zone;
* TABLE time_zone_name;
* TABLE time_zone_transition;
* TABLE time_zone_transition_type;

```
$ mysql_tzinfo_to_sql /usr/share/zoneinfo | mysql -u root -p mysql
```

Then updated **/etc/mysql/my.cnf** and added at the bottom

```
[mysqld]
default_time_zone = Europe/Paris
```
And finally 
```
$ sudo service mysql restart
```



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
To grant it all the rights I used user/paswword found in 
```
less /etc/mysql/debian.cnf (debian-sys-maint)
```


