=====
TomEE
=====

| Apache TomEE a.k.a **Tommy**, is the Java Enterprise Edition of Apache Tomcat, an open-source implementation of the Java Servlet, JavaServer Pages, Java Expression Language and WebSocket technologies. Tomcat provides a Java HTTP web server environment in which Java code can run.
| 
| The webprofile version of TomEE is optimized for JEE [#]_ web applications, which is the case of the app developed in Spring  


Deployment
==========

| First I tried using TomEE in a CentOS 8 container but there was some errors due to container privileges and the way CentOS works. In this case I used Debian which also runs pretty smooth since the Proxmox OS is Debian as well.
| 
| The first TomEE requirement is installing **Java**. In this case I considered using the AdoptOpenJDK8 version of the Java Development Kit and Java Runtime Environment.
| The installation and set up was done as it follows.

.. code-block:: bash

   cd mkdir /usr/lib/jvm/open-jdk-11
   wget https://github.com/AdoptOpenJDK/openjdk8-binaries/releases/download/jdk8u252-b09/OpenJDK8U-jdk_x64_linux_hotspot_8u252b09.tar.gz
   wget https://github.com/AdoptOpenJDK/openjdk8-binaries/releases/download/jdk8u252-b09/OpenJDK8U-jre_x64_linux_hotspot_8u252b09.tar.gz
   tar -xf OpenJDK8U-jdk_x64_linux_hotspot_8u252b09.tar.gz
   tar -xf OpenJDK8U-jre_x64_linux_hotspot_8u252b09.tar.gz
   export PATH=$PWD/jdk8u252-b09/bin:$PATH
   export PATH=$PWD/jdk8u252-b09-jre/bin:$PATH

| After the JRE and JDK were installed, then I installed TomEE.

.. code-block:: bash

   sudo groupadd tomcat
   sudo useradd -s /bin/false -g tomcat -d /opt/tomee tomcat
   wget https://apache.brunneis.com/tomee/tomee-8.0.1/apache-tomee-8.0.1-webprofile.tar.gz
   sudo mkdir /opt/tomee
   sudo tar xzvf apache-tomee-8.0.1-webprofile.tar.gz -C /opt/tomee --strip-components=1
   sudo chgrp -R tomcat /opt/tomee
   sudo chmod -R g+r conf
   sudo chmod g+x conf
   sudo chown -R tomee webapps/ work/ temp/ logs/
   sudo nano /etc/systemd/system/tomcat.service

| Edit the *tomcat.service* file as it follows.

.. code-block:: vim

   [Unit]
   Description=Tomee 8 servlet container
   After=network.target

   [Service]
   Type=forking

   User=tomcat
   Group=tomcat

   Environment="JAVA_HOME=/usr/lib/jvm/jdk8u252-b09"
   Environment="JAVA_OPTS=-Djava.security.egd=file:///dev/urandom"

   Environment="CATALINA_BASE=/opt/tomee"
   Environment="CATALINA_HOME=/opt/tomee"
   Environment="CATALINA_PID=/opt/tomee/temp/tomcat.pid"
   Environment="CATALINA_OPTS=-Xms512M -Xmx1024M -server -XX:+UseParallelGC"

   ExecStart=/opt/tomee/bin/startup.sh
   ExecStop=/opt/tomee/bin/shutdown.sh

   [Install]
   WantedBy=multi-user.target

| The *CATALINA_OPTS* are Java arguments to modify the Java server resources, just like the Minecraft server.
| Finally reload the daemons list so **systemctl** can find the new service and start it.

.. code-block:: bash

   sudo systemctl daemon-reload
   sudo systemctl start tomcat

| The web application must be in *.war* format, not as *.jar*. Deploying the app is easy as placing it in the *webapps* folder. TomEE automatically will detect it and deploy it, creating a new folder with the same name as the app name.
| 
| To access the application I just used the browser and typed the socket address. The default port for TomEE is **8080**.
| 
| 
| 

.. rubric:: *Footnotes*
.. [#] Java Enterprise Edition
