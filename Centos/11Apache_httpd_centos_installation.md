:red_square: __Installing httpd in centos 7__

update the server
```
# yum update -y
```
install the httpd package
```
# yum install httpd
# systemctl start httpd
# systemctl enable httpd
# systemctl status httpd
```
check the status of firewalls
```
# systemctl status firewalld
```
By default, CentOS 7 built-in firewall is set 
to block Apache traffic. To allow web traffic 
on http, set firewall rules to permit inbound 
packets on HTTP and HTTPS for http port 80 
and https port 443

To allow port 80 in firewalld rule
```
# firewall-cmd --permanent --zone=public --add-port=80/tcp
or 
# firewall-cmd --zone=public --permanent --add-service=http
```
To allow port 443 or https in firewalld rule
```
# firewall-cmd --permanent --zone=public --add-port=443/tcp
or
# firewall-cmd --zone=public --permanent --add-service=https
```
reload the firewall service
```
# firewall-cmd --reload
```
create our own index.html file
```
# echo "<h1>Welcome to Tamil Linux Community</h1>" > /var/www/html/index.html
```
restart the apache httpd webserver
```
# systemctl restart httpd.service
```

check in browser
http://server-name or ip

configuration file
```
# vim /etc/httpd/conf/httpd.conf
```
To run syntax check for config files
```
# httpd -t
```
loaded modules
```
# httpd -M
```
log files
```
# tail -f /var/log/httpd/access.log
# tail -f /var/log/httpd/error.log
```

:red_square: __Run Apache httpd webserver in customized port__

By default http runs on port 80 and https runs on port 443

if we want to run apache server in customized port other than 80
for example to run apache server in port 8001 instead of 80

open the file
```
# vim /etc/httpd/conf/httpd.conf
Listen 80
change it to
Listen 8001
:wq! save and exit
```
install selinux package
```
# yum install policycoreutils -y
```
make the selinux policy to allow port 8001
```
# semanage port -a -t http_port_t -p tcp 8001
# semanage port -m -t http_port_t -p tcp 8001
```
restart the server
```
# systemctl restart httpd
```
allow the firewalld rules for 8001 port
```
# firewall-cmd --permanent --zone=public --add-port=8001/tcp
```
reload the firewalld
```
# firewall-cmd --reload
```
in browser
\
http://server_ip:8001
