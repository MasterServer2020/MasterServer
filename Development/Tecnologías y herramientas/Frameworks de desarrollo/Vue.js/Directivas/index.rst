==========
Directivas
==========

| Las directivas son atributos especiales con el prefijo v-. Se espera que los valores de atributo de la directiva sean una única expresión de JavaScript (con la excepción de v-for).
| 
| Las dos directivas más usadas en Vue son: v-bind y v:on, estas tienen una abreviatura usando “:” y “@” respectivamente.

V-bind
======

| Para poder dar valor a un atributo se utiliza la directiva “v-bind”.

------------
Sin abreviar
------------

.. code-block:: html

		<p v-bind:id="id">...</p>

---------
Abreviado
---------

.. code-block:: html

		<p :id="id">...</p>

V-on
====

| Para poder lanzar un evento se utiliza la directiva “v-on”.

------------
Sin abreviar
------------

.. code-block:: html

		<p v-on:click="doTheJob">...</p>
		
---------
Abreviado
---------

.. code-block:: bash

		<p @click="doTheJob">...</p>

