======
Apache
======

| Apache is the most used and famous web server software.

----------
Deployment
----------

| I installed Apache in a CentOS 8 container. Apache is called **httpd** in CentOS, which is the Apache daemon. To install it I simply executed the following commands.

.. code-block:: bash

   yum install httpd
   systemctl start httpd
   systemctl enable httpd


| I installed **git** with ``yum install git`` and downloaded the webpage with ``git clone``.
| Then I installed **nodejs** to compile the webpage code with ``yum install nodejs``.
| I changed the *.env* file to be listening to the TomEE server with its domain name and port.
| Finally I ran the command ``npm setup`` and ``npm run build`` to compile the web application.
| 
| The compiled files are in the *dist* folder, so I moved them to the /var/www/html directory.
| Also I created a *.htaccess* file to specify the webpage routing. Since Vue uses a single page system, by default reloading or accessing a page typing the url will give an error.
| To avoid that I put the following content.

.. code-block:: apache

   <IfModule mod_rewrite.c>
      RewriteEngine On
      RewriteBase /
      RewriteRule ^index\.html$ - [L]
      RewriteCond %{REQUEST_FILENAME} !-f
      RewriteCond %{REQUEST_FILENAME} !-d
      RewriteRule . /index.html [L]
   </IfModule>

| Then I created a configuration file called *masterserver.conf* in the */etc/httpd/conf.d* with the following content.

.. code-block:: apache

   <VirtualHost *:80>
   ServerName masterserver.serveminecraft.net
   DocumentRoot /etc/httpd/html
   <Directory /etc/httpd/html>
   DirectoryIndex index.html
   AllowOverride All
   Require all granted
   </Directory>
   </VirtualHost>

| The webpage is ready and running.
