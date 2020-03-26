# mysql
Install
https://phoenixnap.com/kb/how-to-install-mysql-on-ubuntu-18-04 Problem with signature.  
Opting for https://linuxize.com/post/how-to-install-mysql-on-ubuntu-18-04/
an earlier version   (5.7)


### Admin
admin mypswd_DB!

### Creating a DB
mysql -u admin -p
```
mysql> CREATE DATABASE phpdb;
```
#### Creating user
```
mysql> CREATE USER 'php_user'@'localhost' IDENTIFIED BY 'the password';
```
