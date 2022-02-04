:red_square: __Let's Encrypt SSL Installation and revoke/delete for Nginx webserver in Ubuntu20.04__


update the server
```
#sudo apt update
```
install Certbot and its Nginx plugin 
```
# sudo apt install certbot python3-certbot-nginx
```
open the Nginx configuration file ,
locate the server_name directive and make sure it is set to your domain name
```
# sudo vim /etc/nginx/sites-available/hashlabs.in

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

Obtain the SSL/TLS Certificate
```
# sudo certbot --nginx -d hashlabs.in -d www.hashlabs.in

Enter email address : your_mail@gmail.com
Terms of Service : A
willing to share your email : N
1: No redirect
2.Redirect - Make all requests redirect to secure HTTPS
select option : 2
```
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
```
# certbot revoke --cert-path /etc/letsencrypt/live/hashlabs.in/cert.pem --key-path /etc/letsencrypt/live/hashlabs.in/privkey.pem
```
and open the file and comment the following parameters
```
# vim /etc/nginx/sites-available/hashlabs.in

    listen 443 ssl; # managed by Certbot
    ssl_certificate /etc/letsencrypt/live/hashlabs.in/fullchain.pem; # managed by Certbot
    ssl_certificate_key /etc/letsencrypt/live/hashlabs.in/privkey.pem; # managed by Certbot
    include /etc/letsencrypt/options-ssl-nginx.conf; # managed by Certbot
    ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem; # managed by Certbot
    
change to

    #listen 443 ssl; # managed by Certbot
    #ssl_certificate /etc/letsencrypt/live/hashlabs.in/fullchain.pem; # managed by Certbot
    #ssl_certificate_key /etc/letsencrypt/live/hashlabs.in/privkey.pem; # managed by Certbot
    #include /etc/letsencrypt/options-ssl-nginx.conf; # managed by Certbot
    #ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem; # managed by Certbot

:wq! save and exit
```
restart the nginx webserver
```
# systemctl restart nginx
```
check the status nginx webserver
```
# systemctl status nginx
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
restart the nginx webserver
```
# systemctl restart nginx
```
check in browser
done! :smile:
