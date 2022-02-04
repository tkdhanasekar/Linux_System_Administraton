:red_square: __Let's Encrypt SSL certificate installation and revoke/delete apache webserver in Ubuntu20.04__

update the server
```
# apt update -y
```
install apache webserver
```
# apt install apache2 -y
```
start the apache webserver
```
# systemctl start apache2
```
enable the apache webserver
```
# systemctl enable apache2
```
check the status of apache webserver
```
# systemctl status apache2
```
check the host ip address
```
# hostname -I
```
map the ip address to domain name in dns management of domain provide 
in my case godaddy

restart the apache webserver
```
# systemctl restart apache2
```
install the required packages for let'sencrypt SSL
```
# sudo apt install certbot python3-certbot-apache
```
obtain and install a certificate for apache
```
#sudo certbot --apache

it will ask for the details

Enter email address: tkdhanasekar@gmail.com
Terms of Service: A
willing to share your email: N
Enter domain name : www.hashlabs.in   ( in my case its www.hashlabs.in )
Select the appropriate number [1-2]: 2 
it will ask options select redirect all traffic to HTTPS give option 2
```
check the domain name for ssl certificate in browser
in browser give
https://ssllabs.com/ssltest/analyze.html?d=www.your_domain_name.com

to view the ssl certificates
```
# cerbot certificates
```
run a Certbot dry run to make sure the syntax is ok
```
# certbot renew --dry-run
```
To renew the certificates
```
# certbot renew
```
Enable Automatic Certificate Renewal
```
# crontab -e

Add a cron job
0 8 * * * /usr/bin/certbot renew --quiet
```

:red_square: __To revoke and delete the Let's Encrypt certificate__
``
# certbot revoke --cert-path /etc/letsencrypt/live/www.hashlabs.in/cert.pem --key-path /etc/letsencrypt/live/www.hashlabs.in/privkey.pem
```
replace www.hashlabs.in with your domain name

disable the following lines by comment them out in the following file
```
# vim /etc/apache2/sites-enabled/000-default-le-ssl.conf

find and change 

SSLCertificateFile /etc/letsencrypt/live/www.hashlabs.in/fullchain.pem
SSLCertificateKeyFile /etc/letsencrypt/live/www.hashlabs.in/privkey.pem
Include /etc/letsencrypt/options-ssl-apache.conf
 
to 

#SSLCertificateFile /etc/letsencrypt/live/www.hashlabs.in/fullchain.pem
#SSLCertificateKeyFile /etc/letsencrypt/live/www.hashlabs.in/privkey.pem
#Include /etc/letsencrypt/options-ssl-apache.conf
:wq! save and exit
```
restart the apache webserver
```
# systemctl restart apache2
```
check the status apache webserver
```
# systemctl status apache2
```
update the server
```
# sudo apt update
```
delete the packages letsencrypt and certbot
```
# sudo apt purge letsencrypt && sudo apt purge certbot
```
remove the letsencrypt directories
```
# sudo rm -rf /etc/letsencrypt
```
restart the server
```
# systemctl restart apache2
```


