===========
Controlador
===========

| Los controladores son los encargados de interpretar las datos de las peticiones que realiza el usuario dependiendo del método y de la ruta implementada.

.. code-block:: java

		@RestController
		public class PlayerController {
			@Autowired
			private PlayerService service;

			@GetMapping("/players")
			public ResponseEntity<List<PlayerModel>> getPlayers() {
				return new ResponseEntity<>(service.getAll(), HttpStatus.OK);
			}

			@GetMapping("/player/{id}")
			public ResponseEntity<PlayerModel> getPlayerById(@PathVariable("id") long id) {
				return new ResponseEntity<>(service.getById(id), HttpStatus.OK);
			}

			@PostMapping(value = "/player")
			public ResponseEntity<PlayerModel> createPlayer(@RequestBody PlayerModel player) {
				return new ResponseEntity<>(service.create(player), HttpStatus.OK);
			}

			@PutMapping("/player/{id}")
			public ResponseEntity<PlayerModel> updatePlayer(@PathVariable("id") long id, @RequestBody PlayerModel player) {
				return new ResponseEntity<>(service.update(id, player), HttpStatus.OK);
			}

			@DeleteMapping("/player/{id}")
			public ResponseEntity<Boolean> deletePlayer(@PathVariable("id") long id) {
				return new ResponseEntity<>(service.delete(id), HttpStatus.OK);
			}
		}

- @RestController: Combina las anotaciones @ResponseBody y @Controller. Indica la clase que hace de handler y convierte la respuesta de cada petición a JSON usando la librería Jackson.
- @Autowired: Permite inyectar los beans automáticamente.
- @GetMapping, @PostMapping, @PutMapping, @DeleteMapping: Indica la ruta y el método de la petición.
- @PathVariable: Indica que un parámetro debe de estar vinculado a un parámetro de la plantilla URI.
- @RequestBody: Indica que un parámetro debe de estar vinculado al valor del cuerpo de la petición.


| La clase ResponseEntity maneja toda la respuesta HTTP incluyendo el cuerpo, cabecera y códigos de estado permitiendo configurar la respuesta que queremos que se envié desde los endpoints.
