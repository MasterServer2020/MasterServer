=======================================
Cómo desarrollar un plugin de Minecraft
=======================================

----------------------------------
Añadir la dependencia del servidor
----------------------------------

| Para poder acceder a las clases que proporciona Bukkit se tiene que añadir la dependencia del servidor de Bukkit que se vaya a implementar.
|
| En este caso vamos a usar Maven para bajar la dependencia de un repositorio.

.. code-block:: xml

			<repositories>
			    <repository>
				<id>spigot-repo</id>
				<url>https://hub.spigotmc.org/nexus/content/repositories/snapshots/</url>
			    </repository>
			</repositories>

			<dependencies>
			    <dependency>
				   <groupId>org.spigotmc</groupId>
				   <artifactId>spigot-api</artifactId>
				   <version>1.15.2-R0.1-SNAPSHOT</version>
				   <scope>provided</scope>
			    </dependency>
			</dependencies>


---------------
Clase principal
---------------

| La clase principal es el punto de entrada para que Bukkit cargue e interactúe con su complemento. Es una clase que extiende de JavaPlugin.

.. code-block:: java

		public class Main extends JavaPlugin {
		    private static final String ENABLED_MESSAGE = "------------------MasterPlugin enabled------------------";
		    private static final String DISABLED_MESSAGE = "------------------MasterPluginDisabled disabled------------------";

		    @Override
		    public void onEnable() {
			Bukkit.getConsoleSender().sendMessage(ENABLED_MESSAGE);
		    }

		    @Override
		    public void onDisable() {
			super.onDisable();
			Bukkit.getConsoleSender().sendMessage(DISABLED_MESSAGE);
		    }

		    @Override
		    public boolean onCommand(CommandSender sender, Command command, String label, String[] args) {
			return super.onCommand(sender, command, label, args);
		    }
		}

- OnEnable: Se ejecuta cuando el plugin se activa.
- OnDisable: Se ejecuta cuando el plugin se desactiva.
- OnCommand: Se ejecuta cuando un jugador escribe algo en el chat que comienza por “/”. Este método permite añadir comandos personalizados y/o modificar el funcionamiento de comandos existentes. Además permite  acceder al objeto jugador que ha ejecutado ese comando.

-------------------
Eventos y listeners
-------------------

| Los listeners permiten escuchar acciones que se realizan en el servidor de minecraft. Por  ejemplo, cuando un jugador entra en el servidor.

.. code-block:: java

			public class OnJoinListener implements Listener {

				public OnJoinListener(Main plugin) {
					plugin.getServer().getPluginManager().registerEvents(this, plugin);
				}

				@EventHandler
				public void onPlayerJoin(PlayerJoinEvent event) {
					Player player = event.getPlayer();
					player.sendMessage("Welcome: " + player.getName());
				}
			}




| Para registrar el listener se tiene que llamar al método registerEvents de la clase principal, y se tienen que pasar como argumentos la clase que va a hacer de listener y la clase del plugin principal.

- @EventHandler: Indica que se pueden vincular eventos a ese método. El tipo de evento se especifica con un argumento. En este caso caso el evento se ejecuta cuando un jugador entra en el servidor.


| Además desde la clase principal en el método onEnable() se tiene instanciar la clase del listener.

.. code-block:: java

		    @Override
		    public void onEnable() {
			 new OnJoinListener(this);
		    }


----------
Plugin.yml
----------

| El archivo plugin.yml es necesario y se debe de ubicar en la raíz del proyecto. Proporciona información esencial a Bukkit para cargar su complemento.

.. code-block:: bash

			name: "MasterPlugin"
			version: "0.1.1"
			main: "com.masterplugin.Main"
			author: "Domingo Álvarez"
			description: "This plugin does so much stuff it can't be contained!"
			api-version: "1.8.8"
			commands:
			  change:
			    usage0: "name color [color] [player_name?]"
			    usage1: "prefix color [color] [player_name?]"
			    usage2: "player rank [player_name]"
			  list:
			    usage0: "colors"
			    usage1: "commands"
			    usage1: "warps"
			  add:
			    usage0: "rank [rank_name]"
			    usage1: "rank permission [rank_name] [permission_name]"
			    usage2: "chat player [chat_name] [player_name]"
			  delete:
			    usage0: "rank permission [rank_name] [permission_name]"
			    usage1: "chat player [chat_name] [player_name]"
			    usage2: "chat [chat_name]"
			  chunksLoaded:
			  warp:
			    usage0: "[warp_name]"
			  ping:
			    usage0: "[player_name?]"
			  tpRandom:
			    usage0: "[player_name?]"
			  create:
			    usage0: "warp [warp_name]"
			  delete:
			    usage0: "warp [warp_name]"
			  warp:
			    usage0: "[warp_name]"
			  seen:
			    usage0: "[player_name?]"
			  ping:
			    usage0: "[player_name?]
			    
- Name: Indica el nombre del plugin.
- Version: Indica la versión del plugin.
- Main: Indica la clase principal del plugin.
- Author: Indica el autor del plugin.
- Description: Indica la descripción del plugin.
- Api-version: Indica la  versión de la API que se ha usado.
- Commands: Contiene los comandos que se han creado.

--------------------------
Cómo acceder a la REST API
--------------------------

HttpClient
----------

| El httpClient es la clase que se encarga de realizar las llamadas HTTP en la API REST. Con esto lo que se hace es guardar y recibir datos de la base de datos.

.. code-block:: java

			public class HttpClient {
				private static final String URL = "http://localhost:8080/";

				private static void request(String path, final String method, Observer<String> observer) {
					CloseableHttpClient httpClient = null;
					try {
						httpClient = HttpClients.createDefault();
						HttpRequestBase requestBase = new HttpRequestBase() {
							@Override
							public String getMethod() {
								return method;
							}
						};
						Header[] newHeaders = { new BasicHeader("Content-type", "application/json"),
								new BasicHeader("Accept", "application/json") };
						requestBase.setURI(new URI(path));
						requestBase.setHeaders(newHeaders);
						CloseableHttpResponse httpResponse = httpClient.execute(requestBase);
						HttpEntity entity = httpResponse.getEntity();
						String result = EntityUtils.toString(entity);
						if (httpResponse.getStatusLine().getStatusCode() >= 400) {
							observer.onFailure(new Throwable(result));
						} else {
							observer.onSuccess(result);
						}
						entity.getContent().close();
					} catch (URISyntaxException | IOException e) {
						observer.onFailure(e.getCause());
					} finally {
						try {
							httpClient.close();
						} catch (IOException e) {
							e.printStackTrace();
						}
					}
				}

				private static <T> void request(String path, final String method, T object, Observer<String> observer) {
					CloseableHttpClient httpClient = null;
					try {
						httpClient = HttpClients.createDefault();
						HttpEntityEnclosingRequestBase requestBase = new HttpEntityEnclosingRequestBase() {
							@Override
							public String getMethod() {
								return method;
							}
						};
						Header[] newHeaders = { new BasicHeader("Content-type", "application/json"),
								new BasicHeader("Accept", "application/json") };
						requestBase.setURI(new URI(path));
						requestBase.setHeaders(newHeaders);
						String json = new Gson().toJson(object);
						requestBase.setEntity(new StringEntity(json));
						CloseableHttpResponse httpResponse = httpClient.execute(requestBase);
						HttpEntity entity = httpResponse.getEntity();
						String result = EntityUtils.toString(entity);
						if (httpResponse.getStatusLine().getStatusCode() >= 400) {
							observer.onFailure(new Throwable(httpResponse.getStatusLine().toString()));
						} else {
							observer.onSuccess(result);
						}
						entity.getContent().close();
					} catch (URISyntaxException | IOException e) {
				    observer.onFailure(e.getCause());
					} finally {
						try {
							httpClient.close();
						} catch (IOException e) {
					e.printStackTrace();
						}
					}

				}
				
				public static void get(String path, String route, Observer<String> observer) {
					request(path + route, "GET", observer);
				}

				public static void get(String route, Observer<String> observer) {
					request(URL + route, "GET", observer);
				}

				public static <T> void post(String path, String route, T object, Observer<String> observer) {
					request(path + route, "POST", object, observer);
				}

				public static <T> void post(String route, T object, Observer<String> observer) {
					request(URL + route, "POST", object, observer);
				}

				public static <T> void update(String path, String route, T object, Observer<String> observer) {
					request(path + route, "PUT", object, observer);
				}

				public static <T> void update(String route, T object, Observer<String> observer) {
					request(URL + route, "PUT", object, observer);
				}

				public static void delete(String path, String route, Observer<String> observer) {
					request(path + route, "DELETE", observer);
				}

				public static void delete(String route, Observer<String> observer) {
					request(URL + route, "DELETE", observer);
				}
			}


--------------------------------------
Cómo ejecutar el plugin en el servidor
--------------------------------------

| Para poder usar el plugin en el servidor necesitamos generar un jar del proyecto. Para eso se va a usar Maven. Lo que tenemos que hacer es anadir lo siguiente en el fichero POM.xml para que el jar incluya las dependencias.

.. code-block:: xml

			<build>
			    <pluginManagement>
			      <plugins>
				<plugin>
				      <artifactId>maven-assembly-plugin</artifactId>
				      <configuration>
					<archive>
					  <manifest>
					    <mainClass>com.masterplugin.Main</mainClass>
					  </manifest>
					</archive>
					<descriptorRefs>
					  <descriptorRef>jar-with-dependencies</descriptorRef>
					</descriptorRefs>
				      </configuration>
			    	 </plugin>
			    	<plugins>
			      </pluginManagement>
			</build>

| Para construir el jar tenemos que ejecutar el siguiente comando

.. code-block:: bash

   mvn clean compile assembly:single

| Esta sería la salida del comando.

.. code-block:: bash

			[INFO] Scanning for projects...
			[INFO] 
			[INFO] ----------------------< com.masterplugin:plugin >-----------------------
			[INFO] Building plugin 0.0.1-SNAPSHOT
			[INFO] --------------------------------[ jar ]---------------------------------
			[INFO]
			[INFO] --- maven-clean-plugin:3.1.0:clean (default-clean) @ plugin ---
			[INFO] Deleting C:\Users\DAlvarez\Documents\workspace-spring-tool-suite\MasterPlugin\target
			[INFO] 
			[INFO] --- maven-resources-plugin:3.0.2:resources (default-resources) @ plugin ---
			[INFO] Using 'UTF-8' encoding to copy filtered resources.
			[INFO] Copying 1 resource
			[INFO] 
			[INFO] --- maven-compiler-plugin:3.8.0:compile (default-compile) @ plugin ---
			[INFO] Changes detected - recompiling the module!
			[INFO] Compiling 23 source files to C:\Users\DAlvarez\Documents\workspace-spring-tool-suite\MasterPlugin\target\classes
			[INFO] 
			[INFO] --- maven-assembly-plugin:2.2-beta-5:single (default-cli) @ plugin ---
			[INFO] ------------------------------------------------------------------------
			[INFO] BUILD SUCCESS
			[INFO] ------------------------------------------------------------------------
			[INFO] Total time:  6.985 s
			[INFO] Finished at: 2020-05-30T18:16:16+02:00
			[INFO] ------------------------------------------------------------------------

| Ahora tenemos que copiar ese jar en la carpeta plugins del propio servidor.
|
| Si el servidor se estaba ejecutando basta con ejecutar el comando /reload en la terminal para cargar el plugin.
