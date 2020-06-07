==========
PostgreSQL
==========

| PostgreSQL es un gestor de bases de datos relacional y orientado a objetos. Su licencia y desarrollo es de código abierto, siendo mantenida por una comunidad de desarrolladores, colaboradores y organizaciones comerciales de forma libre y desinteresadamente.

| Características:


- Presenta un sistema de alta concurrencia: Presenta un sistema denominado MVCC, el cual permite que mientras un proceso escribe una tabla, otros puedan acceder a la misma tabla sin necesidad de verse bloqueados, y cada usuario obtiene una visión consistente.
- Notificaciones a tiempo real: A pesar de que PostgreSQL no fue diseñada para ser una BD que trabaje al 100% en tiempo real, si es posible mantener sincronizado en varios dispositivos un sistema de notificación para cuando se hacen cambios específicos en la base de datos, gracias a las funciones LISTEN, UNLISTEN y NOTIFY.
- Registro y guardado de transacciones: Es capaz de registrar cada transacción en un WAL (Write-Ahead-Log). Esto permite restaurar la base de datos a cualquier punto previamente guardado, una especie de "Checkpoint". Esto permite que no sea necesario realizar respaldos completos de forma frecuente.
- Disparadores: En PostgreSQL, un disparador se define como la ejecución de un procedimiento almacenado, basado en una acción determinada sobre una tabla específica en la base de datos.
