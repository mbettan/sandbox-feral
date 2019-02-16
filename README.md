# sandbox-feral
This how-to guide explains how to configure a sandbox in feral hosting.

Once you have a fresh new slot, you will have to connect in ssh 

First step is to configure nginx
Official guide : https://www.feralhosting.com/wiki/software/nginx
Apache to Nginx: https://github.com/feralhosting/feralfilehosting/tree/master/Feral%20Wiki/HTTP/Updating%20Apache%20to%20nginx

mkdir -p ~/.nginx
After waiting 5 minutes Apache will shut down and nginx will have been auto-configured to be very similar to Apache
ls -la ~/.nginx/conf.d/000-default-server.d

Second step is to install couch potato
https://github.com/feralhosting/feralfilehosting/tree/master/Feral%20Wiki/Software/CouchPotato%20-%20An%20automatic%20NZB%20and%20torrent%20downloader%20for%20Films

wget -qO ~/install.couchpotato http://git.io/3_iozg && bash ~/install.couchpotato
Enter then 1 for Install Program

Third step is to install transmission
https://www.feralhosting.com/slots/antiphates/nuxclass/software/install


Then, configure HTTP access
https://docs.nginx.com/nginx/admin-guide/security-controls/configuring-http-basic-authentication/

Create htpasswd

 mkdir private
 htpasswd -c ~/private/.htpasswd [user]


vi ~/.nginx/conf.d/000-default-server.d/links.conf

location /links {
     auth_basic "Restricted Access";
     auth_basic_user_file /media/sdac1/[username]/private/.htpasswd;
}


/usr/sbin/nginx -s reload -c ~/.nginx/nginx.conf
