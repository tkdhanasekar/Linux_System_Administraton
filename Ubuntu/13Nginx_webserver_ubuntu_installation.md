:red_square: __INSTALLATION OF NGINX WEBSERVER__

update the server
```
# sudo apt-get update
```
install nginx webserver packages
```
# sudo apt-get install nginx
```
check the version
```
# nginx -v
```
start the nginx webserver
```
# sudo systemctl start nginx
```
enable the nginx webserver
```
# sudo systemctl enable nginx
```
check the status webserver
```
# sudo systemctl status nginx
```
check the ip address
```
# hostname -I
xx.xx.xx.xx
```
Test nginx in browser\
http://server_ip\
default page of nginx displayed

map this ip address to domain name in dns management of domain name provider
( in my case i purchase domainname hashlabs.in from godaddy )

Configure a Server Block
```
# mkdir -p /var/www/hashlabs.in/html
```
Configure Ownership and Permissions
```
#chown -R $USER:$USER /var/www/hashlabs.in
#chmod -R 755 /var/www/hashlabs.in
```
Create an index.html File for the Server Block
```
# vim /var/www/hashlabs.in/html/index.html
<h1> welcome to Tamil Linux Community </h1>
:wq! save and exit
```
Create Nginx Server Block Configuration
```
# vim /etc/nginx/sites-available/hashlabs.in
server    {
listen 80;
 
root /var/www/hashlabs.in/html;
index index.html index.htm index.nginx.debian.html;
 
server_name hashlabs.in www.hashlabs.in;
location /          {
try_files $uri $uri/ =404;
      }
}

:wq! save and exit
```
Create Symbolic Link for Nginx to Read on Startup
```
# ln -s /etc/nginx/sites-available/hashlabs.in /etc/nginx/sites-enabled
```
restart the nginx webserver
```
# sudo systemctl restart nginx
```

Test the Configuration for any syntax issue
```
# nginx -t
```
in browser
\
http://hashlabs.in


Location of the main Nginx application files.
```
/etc/nginx/nginx.conf
```
List of all websites configured through Nginx
```
/etc/nginx/sites-available/
```
List of websites actively being served by Nginx.
```
/etc/nginx/sites-enabled
```
Access logs 
```
/var/log/nginx/access.log 
```
error logs
```
/var/log/ngins/error.log
```
To run nginx webserver in customized port 8001 from port 80
open the nginx server block config 
```
# vim /etc/nginx/sites-available/hashlabs.in

change 
Listen 80

to
Listen 8001
:wq! save and exit
```
in browser
\
http://hashlabs.in:8001
