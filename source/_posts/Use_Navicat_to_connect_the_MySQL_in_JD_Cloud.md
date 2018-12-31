---
title: Use_Navicat_to_connect_the_MySQL_in_JD_Cloud
date: 2018-09-17 16:09:52
tags: [Skill]
categories: [Linux, MySQL, Navicat]
---

# Use Navicat to connect the MySQL in JD Cloud involved the Ubuntu16.04 LTS system
Select ubuntu 16.04 LTS system.
username: root
password: ----
to login the webserver

Ubuntu Console type in:
```
apt-get update
apt-get install mysql-server
apt-get install mysql-client
apt-get install libmysqlclient-dev
```
Ubuntu Console type in:
```
mysql –V
service mysql start
service mysql stop
service mysql status
service mysql restart
```
navicat remote connect mysql:
[blog](https://blog.csdn.net/qq_38660693/article/details/81771993)
```
sudo netstat -tap | grep mysql
/etc/init.d/mysql restart
mysql -u root -p
sudo vim /etc/mysql/mysql.conf.d/mysqld.cnf
```
Look at the first row: The mysql database server configutation file: you should find **bind-address = 127.0.0.1** and add **#** in front of the command. 

You should find the ↓ tap in your keyboard and press **i** key. at the bottom of the file, you will find **INSERT** then you can insert **#** to comment the command. 

When you finish the process, you press the **ESC** and press **wq!** restore the result.

Then you should restart the server of MySQL
```
/etc/init.d/mysql restart
netstat -an |grep 3306
sudo service mysql start
sudo service mysql status
```
if can not resolve your problem, you can try this methods.
```
vim /etc/mysql/mysql.conf.d/mysqld.cnf
```
add this command in the last line of the mysqld.cnf file
```
skip-name-resolve

```
Source: https://blog.csdn.net/WuZuoDingFeng/article/details/54638999
