====
Java
====

| Java es un lenguaje de programación orientado a objetos que fue diseñado para tener tan pocas dependencias de implementación como fuera posible permitiendo desarrollar y ejecutar aplicaciones en cualquier dispositivo.

Programación orientada a objetos (POO)
======================================

| La POO es una forma más cercana a como expresaríamos las cosas de la vida real en un lenguaje de programación, se basa en la estructuración del código en clases llamadas objetos, los cuales tienen propiedades y métodos.

Principios de la POO
====================

-----------
Abstracción
-----------

| La abstracción consiste en que un método o una clase diga lo que tiene que hacer pero no cómo hacerlo. Esto se consigue implementando clases abstractas e interfaces.

---------------
Encapsulamiento
---------------

| El encapsulamiento es la forma de hacer que los atributos de las clases se puedan editar sólo a través de métodos. De manera general se hace teniendo las propiedades como privadas y los métodos que las controlan públicos. Comúnmente, se crean un grupo de métodos llamados getters que se encargan de obtener el valor de la propiedad y setters que se encargan de dar valor a la propiedad.
|
| Mantener las clases con este principio permite controlar el cambio de valor que pueda producirse en las variables añadiendo validaciones.

.. code-block:: java

   public class User {
      private String name;
      
      public String getName(){
         return name;
      }

      public void setName(String name){
         if(name.startsWith("S")){
            this.name = name;
         }
      }
   }

--------
Herencia
--------

| La herencia es un mecanismo por el cual una clase puede heredar métodos y atributos de otra clase. Con esto se puede puede utilizar funcionalidad existente sin tener que volver a implementar dicha funcionalidad. Todos las clases por defecto heredan funcionalidad de la clase Object.

Superclase
----------

| Es la clase que pasa la funcionalidad a otra clase para que esta pueda utilizar sus métodos. También es conocida como clase padre.

.. code-block:: java

   public class User {
      private String name;

      public User(String name){
         this.name = name;  
      }
      
      public String getName(){
         return name;
      }

      public void setName(String name){
         this.name = name;
      }
   }

Subclase
--------

| Es la clase que utiliza los métodos y atributos de otra clase para realizar alguna acción específica. También es conocida cómo clase hija.
|
| Para implementar la herencia se usa la palabra reservada “extends” en la definición de la clase hija seguida del nombre de la clase padre. Poder hacer uso de los métodos y/o atributos que proporciona el padre usa la palabra reservada “super”.

.. code-block:: java

   public class Operator extends User {
      private String role;

      public Operator(String name, String role){
         super(name);
         this.role = role;  
      }
      
      public String getRole(){
         return role;
      }

      public void setRole(String role){
         this.role = role;
      }
   }

------------
Polimorfismo
------------

| El polimorfismo es la capacidad de un método, variable u objeto de poseer varias formas.

Polimorfismo de asignación
--------------------------

| El polimorfismo de asignación es el que está más relacionado con el enlace dinámico. Una misma variable referenciada puede hacer referencia a más de un tipo de Clase. El conjunto de clase que pueden ser referenciadas está restringido por la herencia o la implementación.

| La forma natural de instanciar un objeto de la clase Operator sería:

.. code-block:: java

   Operator operator = new Operator();

| Sin embargo, el polimorfismo de asignación permite a una variable declarada como otro tipo  usar otra forma, siempre y cuando haya una relación de herencia o implementación.


.. code-block:: java

   User user = new Operator();

Polimorfismo de sobrecarga
--------------------------

| En el polimorfismo de sobrecarga, dos o más métodos comparten el mismo identificador, pero distinta lista de de argumentos. 

.. code-block:: java

   public void setUsername(String name){
      this.username = name;
   }

   public void setUsername(String name, String lastname){
      this.username = name + lastname;
   }

Polimorfismo de inclusión
--------------------------

| El polimorfismo de inclusión es la capacidad de redefinir por completo un método.
|
| Redefinir un método de una Superclase en una Subclase.

.. code-block:: java

   public abstract class User {
      public abstract void doTheJob();

      public class Operator extends User {
         
         @Override
         public void doTheJob(){
                  
         }      
      }
   }

| Redefinir un método de una interfaz en una clase que lo implemente.

.. code-block:: java

   public interface Operation {
      void doTheJob();
   }

      public class Operator implements Operation {
         
         @Override
         public void doTheJob(){
                  
         }      
      }
   }













