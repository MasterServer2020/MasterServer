===========
Repositorio
===========

| Los repositorios son los encargados de realizar las operaciones(Create, read, update and delete) CRUD de los datos de una entidad. Son interfaces que heredan de la interfaz JpaRepository que es la que contiene los métodos para realizar operaciones CRUD.

.. code-block:: java

		@Repository
		public interface PlayerRepository extends JpaRepository<PlayerModel, Long> {
			Optional<PlayerModel> findByUuid(String uuid);
			Optional<PlayerModel> findByName(String name);
			List<PlayerModel> findByPrefix(String prefix);
		}

- @Repository: Indica que es un objeto de acceso a datos.

| También se pueden declarar métodos propios en la interfaz del repositorio para poder realizar otro tipo de operaciones, cómo el método findByName que busca un jugador por su nombre.
|
| Usando la anotación @ManyToMany podemos suprimir el modelo correspondiente de la tabla resultante  en una relación de  muchos a muchos. 
|
| Los repositorios se usan como intermediarios entre los servicios y la base de datos. Se basan en la utilización ORM (Object Relational mapping) para generar sentencias SQL que hacen las funciones básicas CRUD. Es un modelo de programación para transformar objetos en tablas de la base de datos.




