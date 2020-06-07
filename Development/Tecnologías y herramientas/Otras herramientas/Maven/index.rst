=====
Maven
=====

| Maven es una herramienta para el manejo de dependencias automáticas. Basa su configuración en un archivo XML llamado POM (Project Object Model), el cuál permite guardar la información de todas las dependecias de la aplicación dentro del elemento XML dependencies.
|
| En el siguiente ejemplo se muestra como incluir la dependencia con el módulo de Spring spring-boot-starter-data-jpa, para que, a la hora de compilar y ejecutar la aplicación, Maven la incluyese en el classpath.

.. code-block:: xml

			<dependency>
			    <groupId>com.google.code.gson</groupId>
			    <artifactId>gson</artifactId>
			    <version>2.8.6</version>
			</dependency>


| Además Maven permite compilar, generar ejecutables ‘jar’, ejecutar pruebas unitarias y otro tipo de tareas a través de comandos.
