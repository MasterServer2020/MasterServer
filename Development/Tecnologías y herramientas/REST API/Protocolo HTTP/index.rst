==============
PROTOCOLO HTTP
==============

| HTTP (hypertext Transfer Protocol) es el protocolo de comunicaciones usado en la Web para intercambiar documentos HTML, archivos CSS, Javascript, imágenes y otros recursos similares. El protocolo HTTP sigue un esquema petición-respuesta en donde un navegador web, el cliente del protocolo, envía un mensaje de petición a un servidor web y, en consecuencia el servidor devuelve un mensaje de respuesta. 
|
| En este protocolo, cada mensaje de petición y de respuesta se compone de un conjunto de líneas de texto. Por ejemplo, el mensaje de petición incluye una primera línea de texto que incluye la operación (conocida como método o verbo) que desea ejecutar el cliente, un conjunto de líneas adicionales con campos de encabezado, una línea vacía que representa el final del encabezado y, opcionalmente, el texto del mensaje. Esta simplicidad en el formato de los mensajes ha facilitado el desarrollo de una gran variedad de clientes y servidores web. 
|
| Algunos de los métodos de petición más usados por este protocolo son:

GET
===

| Éste método devuelve la información (en forma de entidad) asociada al recurso identificado con la URI solicitada.
|
| Ejemplo:  GET  /players  HTTP/1.1→ Obtiene todos los jugadores.
| Ejemplo con parámetros: GET /player?name=Federico HTTP/1.1 → Obtiene los jugares cuyo nombre es Federico.

POST
====

| Éste método es usado para que el servidor acepte la entidad enviada como parte de la petición, como un nuevo elemento del recurso asociado a la URI solicitada.
|
| Ejemplo: POST  /player HTTP/1.1 → Crea ese jugador.
|
| El contenido va en el body del request, no aparece nada en la URL, aunque se envía en el mismo formato que con el método GET. Se debe de indicar el Content-Type. Se suele usar en formularios html porque es más seguro que el método GET, para crear un usuario en una base de datos, etc.

PUT
===

| Éste método es usado para que la entidad enviada como parte del request sea guardada bajo la URI solicitada. Si la entidad se refiere a un recurso ya existente, se procesa como una entidad actualizada.
|
| Ejemplo: PUT  /player/1 HTTP/1.1 → Actualiza ese jugador.
|
| En el body del request se tiene que indicar el contenido que se va a actualizar.

DELETE
======

| Este método indica al servidor que el recurso identificado con la URI solicitada debe ser eliminado. Nunca lleva datos en el cuerpo.
|
| Ejemplo: DELETE  /player/1 HTTP/1.1 → Borra ese jugador.

HEAD
======

| Su funcionamiento es idéntico al de GET, con la excepción que no devuelve el cuerpo de la respuesta. Solo se reciben los datos del encabezado.

Códigos HTTP
============

| Los códigos de estado de respuesta HTTP indican si se ha completado satisfactoriamente una solicitud HTTP específica. Las respuestas se agrupan en cinco clases: respuestas informativas, respuestas satisfactorias, redirecciones, errores de los clientes y errores de los servidores. Nos vamos en centrar en los códigos de las respuestas satisfactorias y en los errores de los clientes más usados.

-------------------------
Respuestas satisfactorias
-------------------------

200 OK
------

| La solicitud ha tenido éxito. El significado de un éxito varía dependiendo del método HTTP:

- GET: El recurso se ha obtenido y se transmite en el cuerpo del mensaje.
- HEAD: Los encabezados de entidad están en el cuerpo del mensaje.
- PUT o POST: El recurso que describe el resultado de la acción se transmite en el cuerpo

201 CREATED
-----------

| La solicitud ha tenido éxito y se ha creado un nuevo recurso como resultado de ello. Ésta es típicamente la respuesta enviada después de una petición PUT.

400 NO CONTENT
--------------

| La petición se ha completado con éxito pero su respuesta no tiene ningún contenido, aunque los encabezados pueden ser útiles. El agente de usuario puede actualizar sus encabezados en caché para este recurso con los nuevos valores.

------------------
Errores de cliente
------------------

400 BAD REQUEST
---------------

| Esta respuesta significa que el servidor no pudo interpretar la solicitud dada una sintaxis inválida.

401 UNAUTHORIZED
----------------

| Es necesario autenticar para obtener la respuesta solicitada. Esta es similar a 403, pero en este caso, autenticación es posible.

403 FORBIDDEN
-------------

| El cliente no posee los permisos necesarios para cierto contenido, por lo que el servidor está rechazando otorgar una respuesta apropiada.

404 NOT FOUND
-------------

| El servidor no pudo encontrar el contenido solicitado. Este código de respuesta es uno de los más famosos dada su alta ocurrencia en la web.

405 METHOD NOT ALLOWED
----------------------

| El método solicitado es conocido por el servidor pero ha sido deshabilitado y no puede ser utilizado. Los dos métodos obligatorios, GET y HEAD, nunca deben ser deshabilitados y no debiesen retornar este código de error.
























