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
GRANT SELECT, INSERT, DELETE ON database_name.* TO database_user@'localhost';
