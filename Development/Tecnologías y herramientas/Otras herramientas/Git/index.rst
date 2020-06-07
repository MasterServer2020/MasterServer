===
Git
===

| Git es un software de control de versiones, pensado en la eficiencia y la confibilidad del mantenimiento de versiones de aplicaciones. Su propósito es llevar registro de lo cambios en archivos y coordinador el trabajo que varias personas realizan sobre archivos compartidos.
| 
| Para poder llevar un mejor control del código y de las versiones, se han de usar ramas. Una rama es un espacio independiente para trabajar en un proyecto.
| 
| Ramas que se han usado:

- Master: Rama de producción.
- Develop: Después de realizar pruebas de integración, se integra en Master.
- Feature-XX: Por cada característica a conseguir se va a crear una. Cuando se ha probado, se integra en la rama Develop. Cada tarea se identifica con un código númerico.

Comandos básicos de Git
=======================

--------------------------------
Inicializar el directorio actual
--------------------------------

.. code-block:: bash

   git init

-------------------------------------------------------
Vincular un repositorio remote con el repositorio local
-------------------------------------------------------

.. code-block:: bash

   git remote add origin url/ssh

--------------
Crear una rama
--------------

.. code-block:: bash

   git checkout -b nombre_rama

---------------
Cambiar de rama
---------------

.. code-block:: bash

   git checkout nombre_rama

-----------------------------------------------------------
Anadir todos ficheros nuevos o modificados a la rama actual
-----------------------------------------------------------

.. code-block:: bash

   git checkout nombre_rama

-----------------
Confirmar cambios
-----------------

.. code-block:: bash

   git commit -m "MasterServer-001: Proyecto creado"


------------------------------------------
Enviar los cambios a un repositorio remoto
------------------------------------------

.. code-block:: bash

   git push

-----------------------------------
Fusionar otro rama a la rama activa
-----------------------------------

.. code-block:: bash

   git merge nombre_rama  


