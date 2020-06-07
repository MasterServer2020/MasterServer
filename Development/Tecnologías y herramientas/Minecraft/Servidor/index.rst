========
Servidor
========

| Los servidores de Minecraft permiten a los usuarios jugar en línea con otra gente. Pueden estar alojados en un servidor dedicado, o ser temporales y estar en una máquina doméstica.

| Para poder usar un servidor de minecraft lo que tenemos que hacer es descargar un jar del servidor desde el cliente de minecraft.
|
| Una vez descargado lo ejecutamos y se creará un fichero llamado EULA.txt (acuerdo de licencia de usuario final) que primero debemos aceptar. Para aceptarlo abrimos el archivo y cambios el valor de la propiedad eula por verdadero.

.. code-block:: bash

   eula = true

| Lo siguiente es configurar el fichero server.properties. Dónde tenemos que asignar la ip del servidor de minecraft. Además de que podemos modificar otros parámetros del servidor.

.. code-block:: bash

			#Minecraft server properties
			#Sat May 10 15:46:06 CEST 2020
			spawn-protection=16
			generator-settings=
			force-gamemode=false
			allow-nether=true
			gamemode=0
			broadcast-console-to-ops=true
			enable-query=false
			player-idle-timeout=0
			difficulty=1
			spawn-monsters=true
			op-permission-level=4
			resource-pack-hash=
			announce-player-achievements=true
			pvp=true
			snooper-enabled=true
			level-type=DEFAULT
			hardcore=false
			enable-command-block=false
			max-players=20
			network-compression-threshold=256
			max-world-size=29999984
			server-port=25565
			debug=false
			server-ip=192.168.1.150
			spawn-npcs=true
			allow-flight=false
			level-name=world
			view-distance=10
			resource-pack=
			spawn-animals=true
			white-list=false
			generate-structures=true
			online-mode=true
			max-build-height=256
			level-seed=
			enable-rcon=false
			motd=A Minecraft Server

| Para poder ver la consola y para poder añadir más memoria RAM al servidor, creamos un script con el siguiente contenido.

.. code-block:: bash

   java -Xms8G -Xmx8G -jar server.jar


| Una vez hecho esto ya podemos ejecutar el script y se iniciará el servidor.

.. code-block:: bash

		D:\MasterServer>java -Xms8G -Xmx8G -jar server.jar
		Loading libraries, please wait...
		[15:46:06 INFO]: Starting minecraft server version 1.8.8
		[15:46:06 INFO]: Loading properties
		[15:46:06 INFO]: Default game type: SURVIVAL
		[15:46:06 INFO]: This server is running CraftBukkit version git-Spigot-db6de12-18fbb24 (MC: 1.8.8) (Implementing API version 1.8.8-R0.1-SNAPSHOT)
		[15:46:06 INFO]: Debug logging is disabled
		[15:46:06 INFO]: Server Ping Player Sample Count: 12
		[15:46:06 INFO]: Using 4 threads for Netty based IO
		[15:46:06 INFO]: Generating keypair
		[15:46:06 INFO]: Starting Minecraft server on 192.168.1.150:25565


