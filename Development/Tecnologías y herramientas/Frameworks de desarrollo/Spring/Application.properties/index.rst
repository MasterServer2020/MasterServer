======================
Application.properties
======================

| Spring usa un fichero para la configuración de diferentes parámetros de la aplicación. Estos parámetros deben de ser pares clave-valor. Este fichero se debe de ubicar dentro de la carpeta de recurso src/main/resources con el nombre de application.properties.

.. code-block:: bash

   #Postgres config
   spring.datasource.url = jdbc:postgresql://192.168.1.165/masterserver
   spring.datasource.username = postgres
   spring.datasource.password = admin
   #Hibernate config
   spring.jpa.properties.hibernate.jdbc.lob.non_contextual_creation = true
   spring.jpa.properties.hibernate.dialect = org.hibernate.dialect.PostgreSQLDialect
   spring.jpa.hibernate.ddl-auto = update
   spring.jpa.open-in-view = false
   file.upload-dir = /home/dalvarez/Documents/uploads

| Además se pueden definir parámetros propios para después usarlos en la aplicación. Cómo por ejemplo el parámetro file.upload-dir.

---------------------------
Acceso a parámetros propios
---------------------------

Usando la anotación @Value
---------------------------

La anotación @Value enlaza la propiedad que se indica en el atributo anotado.

.. code-block:: java

   @Value("${file.upload-dir}")
   private String fileUploadDir;


Usando una clase POJO
---------------------

| La anotación @ConfigurationProperties enlaza el prefijo de la propiedad que se indica con la clase POJO anotada.

.. code-block:: java

   @ConfigurationProperties(prefix = "file")
   public class FileStorageProperties{
      private String uploadDir;
      
      public String getUploadDir(){
         return uploadDir;
      }

      public String setUploadDir(String uploadDir){
         this.uploadDir = uploadDir;     
      }
   }

| Además en la clase Principal se tiene que usar la anotación @EnableConfigurationProperties indicando las clases de configuración que se quieran habilitar para usar esta catacterística.

.. code-block:: java

   @EnableConfigurationProperties({FileStorageProperties.class})
   @SpringBootAplication
   public class MasterRestApi{
      public static void main(String[] args){
         SpringApplication.run(MasterRestApi.class, args);
      }
   }
















