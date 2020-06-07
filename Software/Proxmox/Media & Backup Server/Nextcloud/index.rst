=========
Nextcloud
=========

| **Nextcloud** is an open source project to create your own self managed cloud without any restrictions. 
| 
| Most cloud services offer a free plan that only include a small amount of storage, but if more space is required users must pay.
| The best free and most widespread option is Google Drive, which offers only 15GB for free. Extra space is a monthly paid feature.
| The only limit on NextCloud is the amount of storage the user wants to buy in form of HDDs or SSDs.

Deployment
==========

| The cloud is going to be hosted in a CentOS 8 container with the */zpool/data/cloud* mount point.
| First im going to install the requirements, which are httpd, php, mariadb and redis.

.. code-block:: bash

   dnf update -y
   dnf install -y epel-release yum-utils unzip curl wget bash-completion policycoreutils-python-utils mlocate bzip2
   dnf install -y httpd
   systemctl enable httpd.service
   systemctl start httpd.service

   dnf install https://rpms.remirepo.net/enterprise/remi-release-8.rpm
   dnf install yum-utils
   dnf module reset php
   dnf module install php:remi-7.4
   dnf update
   dnf install -y php php-gd php-mbstring php-intl php-pecl-apcu\
        php-mysqlnd php-opcache php-json php-zip

   dnf install -y mariadb mariadb-server
   systemctl enable mariadb.service
   systemctl start mariadb.service
   mysql_secure_installation

   dnf install -y redis
   systemctl enable redis.service
   systemctl start redis.service

| Then I downloaded the NextCloud zip file, placed it in the html folder so it can be deployed in the web server and assigned its permissions.

.. code-block:: bash

   wget https://download.nextcloud.com/server/releases/nextcloud-18.0.4.zip
   unzip nextcloud-*.zip
   cp -R nextcloud/ /var/www/html/
   mkdir /var/www/html/nextcloud/data
   chown -R apache:apache /var/www/html/nextcloud
   systemctl restart httpd.service

| Nextcloud is set up and ready to run.
