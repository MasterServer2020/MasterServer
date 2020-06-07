===============
Interpolaciones
===============

Texto
===============

| Una forma de enlazar datos a la vista es mediante la sintaxis de Bigote(llaves dobles).

.. code-block:: html

		<p>{{hello}}</p>

| La propiedad hello será reemplazada por su valor correspondiente, y si en algún momento este se modifica, se actualizará la vista con el nuevo valor.

Expresiones JavaScript
======================

| Vue permite utilizar expresiones de Javascript para interpretar nuestros datos, como por ejemplo el operador ternario.

.. code-block:: html

		<p>{{id > 0 ? id : -1}}</p>
