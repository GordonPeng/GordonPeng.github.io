# Linus必知软件

## Web服务软件

nginx

### apache

yum clean all

yum -y update

yum -y install httpd

systemctl enable httpd.service 

systemctl start httpd.service

配置虚拟主机

mkdir -p /var/www/包名/public_html

chown -R apache/apache /var/www/包名/public_html

chmod -R 755 /var/www

粘贴源代码

配置Apache配置文件

mkdir  /etc/httpd/sites-available

mkdir  /etc/httpd/sites-enabled

vim  /etc/httpd/conf/httpd.conf

增加--> IncludeOptionl site-enabled/*.conf











### 









### IIS





## 数据库软件

MySQL

MongoDB

Oracle

Redis

## 脚本解释器

java

php

asp

node.js

python

## 安全软件

## 辅助软件

编辑器

压缩解压



