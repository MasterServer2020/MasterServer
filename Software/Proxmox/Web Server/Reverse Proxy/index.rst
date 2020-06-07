===================
Nginx Reverse Proxy
===================

| **Nginx** is the original reverse proxy server.
| 
| A reverse proxy is a server that handles all the petitions from internet to a single or multiple web servers in the network.
| Its benefits are the following.

- Anonimation of original web servers
- Protection
- Cache
- DNS & SSL management

Deployment
==========

| The Nginx reverse proxy is going to be deployed in a CentOS 8 container.
| To install it simply run the following commands.

.. code-block:: bash

   dnf install nginx
   systemctl enable nginx
   systemctl start nginx

| I created the */etc/nginx/conf.d/proxy.conf* file with the proxy reverse proxy configuration. The simple configuration I made is as easy as it follows.

.. code-block:: nginx

   server {
       server_name masterserver.serveminecraft.net;
       location / {
           proxy_pass http://192.168.0.126:80;
       }
   }

   server {
       server_name masterstats.serveminecraft.net;
       location / {
           proxy_pass http://192.168.0.115:3000;
       }
   }

| That configuration is enough to have both domain names targeting to different web servers that are only visible in the private network.

-------
Certbot
-------

| Certbot is a free SSL certificate manager, a **Let's Encrypt** CA [#]_ client that uses the ACME [#]_ protocol.
| Its compatible with the most popular web server software, free and easy to set up.
| To install it I executed the following commands.

.. code-block:: bash

   curl -O https://dl.eff.org/certbot-auto
   mv certbot-auto /usr/local/bin/certbot-auto
   chmod 0755 /usr/local/bin/certbot-auto
   certbot-auto --nginx -d masterserver.serveminecraft.net -d masterstats.serveminecraft.net

| Then I chose the option *2: Secure*, so certbot will modify the configuration file and the web servers will only be accessible using HTTPS.
| 
| Finally I added a **crontab** entry with ``crontab -e`` to automatically renew the certificate everyday at 10 am so it won't expire.

.. code-block:: vim

   0 10 * * * /usr/local/bin/certbot-auto renew --quiet

.. rubric:: *Footnotes*

.. [#] Certificate Authority
.. [#] Automatic Certificate Management Environment
