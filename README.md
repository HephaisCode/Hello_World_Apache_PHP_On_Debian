# Hello World Apache On Debian
[![OS badge](https://img.shields.io/badge/OS-Debian-red.svg)](https://www.debian.org)
[![Server badge](https://img.shields.io/badge/Server-Apache-blue.svg)](https://httpd.apache.org)
[![Language badge](https://img.shields.io/badge/Language-PHP-blue.svg)](https://php.net)
[![Format badge](https://img.shields.io/badge/Format-HTML-green.svg)](https://lyty.dev/html/index.html)

## Objectif 

Create page HTML for **hello-world.hephaiscode.com** with Apache and PHP File. PHP file use HTML format.

## You need

- Server on Debian (linux distribution) with root access
- DN (Domain Name) point on Server IP (example hello-world.hephaiscode.com on 51.83.45.10)
- Terminal/console to enter instruction

## Parameters

We use :
 - hello-world.hephaiscode.com for domain name of our web page
 - 51.83.45.10 the IP address of our server computer

## Connect to server 

Open terminal or console and go to admin your server.

```
ssh -l root 51.83.45.10 
```

And enter your root password 

## Update your server

Always to be update.

```
apt-get update
apt-get -y upgrade
apt-get -y dist-upgrade
```

## Install Apache

Install Apache as WebServer to communicate with your server at **hello-world.hephaiscode.com **

```
apt-get -y install apache2
systemctl restart apache2
```
## Install PHP

Install PHP with Apache

```
apt-get -y install php7.3-fpm
a2dismod php7.3
a2enconf php7.3-fpm
a2enmod proxy_fcgi
systemctl restart apache2
```
## Install Domain Name

Create the host parameters for Apache and our domains **hello-world.hephaiscode.com**

```
mkdir /home/helloworld
rm /etc/apache2/sites-available/helloworld_ws.conf
echo "<VirtualHost *:80>" >> /etc/apache2/sites-available/helloworld_ws.conf
echo "Protocols h2 http/1.1" >> /etc/apache2/sites-available/helloworld_ws.conf
echo "ServerAdmin contact@helloworld.io" >> /etc/apache2/sites-available/helloworld_ws.conf
echo "ServerName hello-world.hephaiscode.com" >> /etc/apache2/sites-available/helloworld_ws.conf
echo "ServerAlias hello-world.hephaiscode.com" >> /etc/apache2/sites-available/helloworld_ws.conf
echo "DocumentRoot /home/helloworld" >> /etc/apache2/sites-available/helloworld_ws.conf
echo "<Directory />" >> /etc/apache2/sites-available/helloworld_ws.conf
echo "AllowOverride All" >> /etc/apache2/sites-available/helloworld_ws.conf
echo "</Directory>" >> /etc/apache2/sites-available/helloworld_ws.conf
echo "<Directory /home/helloworld>" >> /etc/apache2/sites-available/helloworld_ws.conf
echo "Options Indexes FollowSymLinks MultiViews" >> /etc/apache2/sites-available/helloworld_ws.conf
echo "AllowOverride all" >> /etc/apache2/sites-available/helloworld_ws.conf
echo "Require all granted" >> /etc/apache2/sites-available/helloworld_ws.conf
echo "</Directory>" >> /etc/apache2/sites-available/helloworld_ws.conf
echo "LogLevel error" >> /etc/apache2/sites-available/helloworld_ws.conf
echo "ErrorLog /var/log/apache2/helloworld-error.log" >> /etc/apache2/sites-available/helloworld_ws.conf
echo "CustomLog /var/log/apache2/helloworld-ssl-access.log combined env=NoLog" >> /etc/apache2/sites-available/helloworld_ws.conf
echo "</VirtualHost>" >> /etc/apache2/sites-available/helloworld_ws.conf
a2ensite helloworld_ws.conf
systemctl restart apache2
```

## File Script
Write root's file in HTML. The name is index.html
```
rm /home/helloworld/index.php
echo '<html><body><?php echo("Hello World!");?></body></html>' >> /home/helloworld/index.php
```
```
rm /home/helloworld/phpinfo.php
echo '<html><body><?php phpinfo();?></body></html>' >> /home/helloworld/phpinfo.php
```

## Hello World Success
Open browser and go to page http://hello-world.hephaiscode.com 

![Success](https://img.shields.io/badge/Hello%20World-OK-Green.svg)
