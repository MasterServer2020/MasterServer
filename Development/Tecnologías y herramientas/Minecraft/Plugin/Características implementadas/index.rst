=============================
Características implementadas
=============================

| Algunas de las características que se han implementado son las siguientes.

Mensaje de bienvenida
=====================

| Al entrar en el servidor se muestra un mensaje de bienvenida mostrando el rango y el nombre del jugador.

.. image:: media/welcome.png
   :width: 400px
   :align: center

Sistema de rangos
=================

| Se usa para autorizar a los jugadores a usar los recursos y/o comandos que ejecuten.
| 
| De momento los rangos que se usan son miembro y dueño.

Guardar los logros de un jugador
=================================

| Los logros son una forma de orientar a los nuevos jugadores de Minecraft y proponer desafíos a completar.
| 
| Cuando se realiza ese evento, el logro que ha conseguido el jugador se guarda en la base de datos.

.. image:: media/achievement_unlock.png
   :width: 400px
   :align: center
   
Comandos
========

| Lo que está entre llaves son los parámetros del comando.

-----
/ping
-----

| Comprueba la latencia del jugador con el servidor.

.. image:: media/ping_self.png
   :width: 225px
   :align: center

----------------------
/ping {nombre_jugador}
----------------------

| La diferencia con el comando anterior es que se comprueba la latencia del jugador que se indica.
| 
| El jugador requiere tener el rango dueño.

.. image:: media/ping_other.png
   :width: 300px
   :align: center
   
--------------------------
/create warp {nombre_warp}
--------------------------

| Crea un checkpoint para que un jugador se pueda teletransportar en cualquier momento.

| Los jugadores con el rango miembro sólo pueden crear 1 warp mientras que los jugadores con el rango dueño pueden crear 2 warps.

.. image:: media/create_warp.png
   :width: 300px
   :align: center
   
--------------------------
/warp {nombre_warp}
--------------------------

| El jugador se transporta a las coordenadas de ese warp automáticamente.

.. image:: media/warp.png
   :width: 400px
   :align: center
      
--------------------------
/delete warp {nombre_warp}
--------------------------

| Borra un warp creado anteriormente.

.. image:: media/delete_warp.png
   :width: 225px
   :align: center
   
-----------
/list warps
-----------

| Muesta una lista con el nombre de los warps creados.

.. image:: media/list_warps.png
   :width: 225px
   :align: center
      
---------------------------------
/change name color {nombre_color}
---------------------------------

| Cambia el color del nombre del jugador. Sólo el jugador con el rango dueño puede usar el color arcoiris.

.. image:: media/change_name_color.png
   :width: 400px
   :align: center

| 
   
.. image:: media/change_name_color_tab.png
   :width: 400px
   :align: center

--------------------------------------------------
/change name color {nombre_color} {nombre_jugador}
--------------------------------------------------

------------
/list colors
------------

| Muestra los colores disponibles.

.. image:: media/list_colors.png
   :width: 400px
   :align: center
   
-----
/seen
-----

| Muestra la fecha en la que el jugador se ha conectado al servidor por última vez.

.. image:: media/seen.png
   :width: 400px
   :align: center

----------------------
/seen {nombre_jugador}
----------------------

| La diferencia con el comando anterior es que muesta la fecha del jugador que se indica.
| 
| El jugador requiere tener el rango dueño.


-------------
/chunksLoaded
-------------

| Muestra la parte que está carga del mapa del servidor.
| 
| El jugador requiere tener el rango dueño.


Errores personalizados al ejecutar un comando
=============================================

----------------------------
Comando con pocos argumentos
----------------------------

.. image:: media/too_few.png
   :width: 300px
   :align: center
   
---------------------------------
Comando con demasiados argumentos
---------------------------------

.. image:: media/too_many.png
   :width: 325px
   :align: center
   
----------------------------------
Comando con argumentos incorrectos
----------------------------------

.. image:: media/wrong.png
   :width: 250px
   :align: center
   
--------------------------------
Si el jugador no está autorizado
--------------------------------

.. image:: media/permission.png
   :width: 400px
   :align: center

















