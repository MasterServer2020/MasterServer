==========
PostgreSQL
==========

| **PostgreSQL** is an open source relational database for Unix OSs, macOS and Windows.

Deployment
==========

| It's going to be deployed in a CentOS 8 container. After being deployed I removed the gateway IP for security reasons.
| 
| To install PostgreSQL I added its repository, disabled the built-in PostgreSQL module, installed the packages and initiated the database.

.. code-block:: bash

   sudo yum -y install https://download.postgresql.org/pub/repos/yum/reporpms/EL-8-x86_64/pgdg-redhat-repo-latest.noarch.rpm
   sudo dnf -qy module disable postgresql
   sudo dnf -y install postgresql12 postgresql12-server
   sudo /usr/pgsql-12/bin/postgresql-12-setup initdb
   sudo systemctl enable --now postgresql-12

| Once it was installed I added a new user which is going to be used to manage the database and created the database.

.. code-block:: bash

   sudo su - postgres
   psql -c "alter user postgres with password 'password'" 
   psql -c "create database masterserver"

| I edited the */var/lib/pgsql/12/data/postgresql.conf* file to specify which addresses it will listen to. Setting it to all will work properly, since a single IP didn't work for the plugin.

.. code-block:: vim

   listen_addresses = '*'

| Finally I edited the */var/lib/pgsql/12/data/pg_hba.conf* file and added the following entry to accept remote connections from the subnet.

.. code-block:: vim

   # Accept from trusted subnet
   host all all 192.168.18.0/24 md5
