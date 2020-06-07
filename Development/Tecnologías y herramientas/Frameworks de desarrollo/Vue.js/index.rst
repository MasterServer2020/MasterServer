======
Vue.js
======

| Vue es un Framework progresivo para construir interfaces de usuario. A diferencia de otros Frameworks monolíticos, Vue está diseñado desde cero para ser utilizado incrementalmente. La librería central está enfocada solo en la capa de visualización, y es fácil de utilizar e integrar con otras librerías o proyectos existentes. Por otro lado, Vue también es perfectamente capaz de impulsar sofisticadas Single-Page Applications (SPA ) cuando se utiliza en combinación con herramientas modernas y librerías de apoyo.
|
| Una de las principales características de este framework es la reactividad, eso quiere decir que si cambia una variable en una parte de la vista de la página, Vue actualizará su nuevo valor sin necesidad de que lo hagas manualmente.

Instalación
===========

| Npm es el método de instalación recomendado para construir  una SPA.
|
| Para instalar Vue de esta manera, primero se necesita instalar NodeJS y NPM. Una vez instalado, bastaría con lanzar el siguiente comando en la terminal.

.. code-block:: bash

   npm install vue

| Vue nos ofrece una interfaz de línea de comandos (CLI) que está compuesta por muchas herramientas que nos permiten elegir qué dependencias o librerías queremos usar en nuestro proyecto.

.. code-block:: bash

   npm i -g @vue/cli	
   
| Para crear un proyecto tenemos que ejecutar el siguiente comando.

.. code-block:: bash

   vue create prueba
   
| Este nos dará una opción a escoger entre una configuración manual o por defecto.

.. code-block:: bash

   ? Please pick a preset: (Use arrow keys)
   > default (babel, eslint)
     Manually select features


.. toctree::
   :caption: Contents
   :maxdepth: 1
	
   Componentes/index
   Interpolaciones/index
   Directivas/index
   Propiedades computadas, observadores y métodos/index
   Navegación/index
   Servicios y Vuex/index
   Internacionalización/index
   Diseño de la aplicación/index












