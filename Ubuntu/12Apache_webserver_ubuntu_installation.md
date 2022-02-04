:red_square: __Installing apache2 webserver in Ubuntu 20.04__

update the system
```
# apt update -y
```
install the apache2 package
```
# apt install apache2 -y
```
To start the apache server
```
# systemctl start apache2
```
To make apache server run persistent across reboots
```
# systemctl enable apache2
```
To check the apache server status
```
# systemctl status apache2
```
To check for ufw firewall status
```
# ufw status
```
To run apache default page in browser
```
http://server_ip
```
move the default documentroot to /opt
```
# mv /var/www/html/index.html /opt
```
create your own index.html file
```
# vim /var/www/html/index.html

<h1> Welcome to Tamil Linux Community </h1>
:wq! save and quit
```
in browser
http://server_ip

configuration file
```
# vim /etc/apache2/apache2.conf
```
configuration test
```
# apachectl -t
or 
# apachectl configtest
```
To view loaded modules
```
# apachectl -M
```
log files location
```
# tail -f /var/log/apache2/access.log
# tail -f /var/log/apache2/error.log
```


:red_square: __To run Apache webserver in customized port:__\
default http port is 80
default https port is 443

if you want to run apache server in customised port other than 80
for example to run apache server in port 8001 instead of 80
open the file
```
#vim /etc/apache2/ports.conf
Listen 80
Change it to
Listen 8001
:wq! save and exit
```

When you change port number in Apache on Ubuntu/Debian systems, 
we need to also change port number in virtual host configuration file
open the file
```
# vim /etc/apache2/sites-enabled/000-default.conf
<VirtualHost: *:80>

change to 

<VirtualHost: *:8001>
:wq! save and exit
```
restart the apache server
```
# systemctl restart apache2
```
in browser check with\
http://server_ip:8001


