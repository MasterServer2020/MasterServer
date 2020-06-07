===========
Componentes
===========

| Los componentes de Vue son instancias reutilizables con nombre único que se declaran mediante una etiqueta HTML, como por ejemplo, <hello/>.
|
| Estos componentes son ficheros con extensión .vue. Están dividios en 3 bloques principales: <template>,<script> y <style>.

.. code-block:: html

		<template>
		    <div>
		    	<p>{{hello}}</p>
		    </div>
		</template>

		<script>
		    export default {
			data(){
			    return {
				hello: 'hey'
			    }
			}
		    }
		</script>

		<style scoped>
		    p {
		    	text-align: center;
		    }
		</style>

| En la etiqueta <template> se declara el código HTML para diseñar la vista del componente, en la apliación se ha usado la librería bootstrap-vue para hacer la aplicación responsive y fontawesome para usar los iconos que nos proporciona, en este bloque podremos añadir las variables del objeto data, métodos...
|
| En la sección <script> podemos definir la lógica de la aplicación y determinar el código que queremos ejecutar durante los ciclos de vida del componente.
|
| Finalmente, en el bloque <style> añadimos los estilos CSS para personalizar el componente.

Sintaxis de una plantilla Vue
=============================

| Vue utiliza una sintaxis de plantilla basada en HTML que permite renderizar declarativamente datos en el DOM. Una de sus principales características es su sistema de reactividad. Como los datos y el DOM están enlazados, al editar el valor de un objeto de JavaScript, la vista se modifica automáticamente.
