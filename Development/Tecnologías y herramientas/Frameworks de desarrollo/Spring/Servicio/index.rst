========
Servicio
========

| Los servicios son los encargados de procesar los datos que reciben de los controladores y de acceder a los repositorios. Además se encargan de controlar los errores que se puedan llegar a producir.

.. code-block:: java

		@Service
		public class PlayerServiceImpl implements PlayerService {
			@Autowired
			private PlayerRepository repository;

			@Override
			public List<PlayerModel> getAll() {
				List<PlayerModel> players = repository.findAll();
				if (players.isEmpty()) {
					throw new ResponseStatusException(HttpStatus.NOT_FOUND, "Players not found.");
				}
				return repository.findAll();
			}

			@Override
			public PlayerModel getById(long id) {
				return repository.findById(id).orElseThrow(() -> new ResponseStatusException(HttpStatus.NOT_FOUND,
						"Id {" + id + "} not found, couldn't get the player."));
			}

			@Override
			public PlayerModel create(PlayerModel player) {
				if (repository.findByName(player.getName()).isPresent()) {
					throw new ResponseStatusException(HttpStatus.CONFLICT,
							"Name {" + player.getName() + "} exists, couldn't create the player.");
				}
				if (repository.findByUuid(player.getUuid()).isPresent()) {
					throw new ResponseStatusException(HttpStatus.CONFLICT,
							"Uuid {" + player.getUuid() + "} exists, couldn't create the player.");
				}
				return repository.save(player);
			}

			@Override
			public boolean delete(long id) {
				repository.findById(id).orElseThrow(() -> new ResponseStatusException(HttpStatus.NOT_FOUND,
						"Id {" + id + "} not found, couldn't delete the player."));
				repository.deleteById(id);
				return true;
			}
		}

- @Service: Indica que es la capa lógica de negocio.

| La clase ResponseStatusException permite lanzar excepciones indicando un código de estado Http, un mensaje y una causa. Esto permite crear excepciones de forma progresiva y además evita crear clases de excepciones propias.
