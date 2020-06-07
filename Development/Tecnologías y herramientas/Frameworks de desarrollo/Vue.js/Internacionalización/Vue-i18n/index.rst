========
Vue-i18n
========

| Vue I18n es el plugin de internacionalización de Vue.js. Integra fácilmente algunas características de localización en una  aplicación de Vue.js.

Instalación usando Cli
======================

| La ventaja de usar Cli es que añade todo lo necesario para que funcione el plugin automáticamente.

.. code-block:: bash

   vue add i18n
  
Añadir traducciones
===================

- En la carpeta src/locales/*nombre*.js con un conjunto de ficheros de traducción.
- En la sección <i18n>  de un componente de archivo único.

| Se pueden usar conjuntamente ambas opciones. La principal diferencia es los archivos JSON son accesibles de forma global mientras que las secciones <i18n> sólo están disponibles en ese componente.

----------------
En archivos .vue
----------------

| Se pueden añadir las traducciones en la sección <i18n>.

.. code-block:: html

			<i18n>
			{
			  "en": {
			    "stats": "Statistics",
			    "achievements": "Achievements",
			    "punishments": "Punishments"
			  },
			  "es": {
			    "stats": "Estadísticas",
			    "achievements": "Logros",
			    "punishments": "Penalizaciones"
			  }
			}
			</i18n>

----------------
En archivos JSON
----------------

En src/locales/en.json (Para las traducciones en Espa)
------------------------------------------------------

.. code-block:: json

			{
			    "stats": "Statistics",
			    "achievements": "Achievements",
			    "punishments": "Punishments"
			}

En src/locales/es.json
----------------------

.. code-block:: json

			{
			    "stats": "Estadísticas",
			    "achievements": "Logros",
			    "punishments": "Penalizaciones"
			}

Usar las traducciones en las plantillas
=======================================

------------
Texto simple
------------

.. code-block:: html

			<p>{{$t('hello')}}</p>

-----------------------
Texto usando parámetros
-----------------------


.. code-block:: html

			<p>{{$t('hello', { name: 'Federico'})}}</p>






