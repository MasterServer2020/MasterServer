======
Spring
======

| Spring es un framework para el desarrollo de aplicaciones  JEE (Java Enterprise Edition). Es el encargado de generar beans a partir de objetos básicos de Java, o clases POJOs (Plain Old Java Objects). Para poder relacionar los beans, Spring usa el concepto de inyección de dependencia a través de la inversión de control. La configuración de los beans se describe mediante ficheros xml. Spring usa anotaciones para poder hacer uso de los propios.

Plain Old Java Object (POJO)
============================

| Un POJO es una clase independiente de cualquier framework. Este tipo de clase no tiene ningún tipo de restricción especial, y se usa para simplificar la estructuración del  desarrollo, reduciendo su complejidad, aumentando la legibilidad y facilitando la reutilización de código.

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

      @Override
      public int compareTo(User user){
         return name.compareTo(user.getName());
      }

      @Override
      public int hashCode(){
         final int prime = 31;
         return prime + ((name == null) ? 0 : name.hasCode());
      }

      @Override
      public boolean equals(Object user){
         User other = (User) user;
         return name.equals(other.getName());
      }   
   } 

.. toctree::
   :caption: Contents
   :maxdepth: 1
	
   Application.properties/index
   Modelo/index
   Repositorio/index
   Servicio/index
   Controlador/index
   Pruebas unitarias/index












