__LAMP stack installation in ubuntu 20.04__


update the server
$ apt update -y

__Apache Installation__


$ sudo apt install apache2 apache2-utils -y
$ systemctl start apache2
$ systemctl enable apache2
$ systemctl status apache2
$ apache2 -v

in browser 
http://server_ip

MariaDB Installation
--------------------

for default 10.3 version of mariadb installation
# apt install mariadb-server mariadb-client -y

or

for mariadb 10.4 version installation follow this steps
# sudo apt-get install software-properties-common
# sudo apt-key adv --recv-keys --keyserver hkp://keyserver.ubuntu.com:80 0xF1656F24C74CD1D8
# sudo add-apt-repository 'deb [arch=amd64,arm64,ppc64el] http://mirror.lstn.net/mariadb/repo/10.4/ubuntu focal main'
# sudo apt update
# sudo apt install mariadb-server
# systemctl status mysql
# mariadb --version

# systemctl enable mariadb
# systemctl status mariadb

# mysql_secure_installation
You already have your root account protected, so you can safely answer 'n'.

Switch to unix_socket authentication [Y/n] n
Change the root password? [Y/n] y
New password: 
Re-enter new password:
Remove anonymous users? [Y/n] y
Disallow root login remotely? [Y/n] y
Remove test database and access to it? [Y/n] y
Reload privilege tables now? [Y/n] y

# mariadb -u root -p

MariaDB [(none)]> CTRL-D

PHP 7.4 Installation
--------------------

install php repo
# sudo add-apt-repository ppa:ondrej/php
# sudo apt update
# apt install php7.4 libapache2-mod-php7.4 php7.4-mysql php-common php7.4-cli php7.4-common php7.4-json php7.4-opcache php7.4-readline -y
# php --version

test php on browser
# vim /var/www/html/info.php
<?php 
phpinfo(); 
?>

in browser
http://server_ip/info.php
