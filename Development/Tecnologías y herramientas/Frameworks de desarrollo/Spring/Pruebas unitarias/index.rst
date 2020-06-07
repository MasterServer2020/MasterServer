=================
Pruebas unitarias
=================

| Los pruebas unitarias verifican el código comprobando si realmente funciona correctamente y asegurando que deban realizar todo lo que esperan que realicen.

.. code-block:: java

		public class PlayerServiceImplTests implements PlayerServiceTests {

			@Mock
			private PlayerRepository repository;

			@InjectMocks
			private PlayerServiceImpl service;

			@BeforeEach
			public void setup() {
				MockitoAnnotations.initMocks(this);
			}

			@Test
			@Override
			public void getAll() {
				Mockito.when(repository.findAll()).thenReturn(new ArrayList<PlayerModel>());
				Assertions.assertThrows(ResponseStatusException.class, () -> {
					List<PlayerModel> players = service.getAll();
					Assertions.assertNull(players);
				});
				Mockito.verify(repository, Mockito.times(1)).findAll();
			}

			@Test
			@Override
			public void getById() {
				PlayerModel player = new PlayerModel(1l, "8c898aa3-b0fb-4695-82fc-a816a7a3c3ec", "Federico",
				"[Dev]", "&3", "&l", "&4", "&l", CustomDate.getCurrentDate(), CustomDate.getCurrentDate(),
				1232312l, "17.212.1");
				Mockito.when(repository.findById(Mockito.anyLong())).thenReturn(Optional.of(player));
				PlayerModel result = service.getById(Mockito.anyLong());
				Mockito.verify(repository, Mockito.times(1)).findById(Mockito.anyLong());
			}

			@Test
			@Override
			public void delete() {
				Assertions.assertThrows(ResponseStatusException.class, () -> {
					service.delete(Mockito.anyLong());
				});
				Mockito.verify(repository, Mockito.times(1)).findById(Mockito.anyLong());
				Mockito.verify(repository, Mockito.times(0)).deleteById(Mockito.anyLong());
			}
      }


- @Mock: Permite convertir un objeto en un Mock.
- @InjectMocks: Permite inyectar al objeto anotado los Mocks creados en esa clase.
- @BeforeEach: Esta anotación permite ejecutar el método anotado antes de cada método anotado por la anotación @Test.
- @Test: Define el método que se puede ejecutar como un caso de prueba.

| Los mock objects simulan parte del funcionamiento de una clase, esto se hace para evitar acceder a alguna capa de nuestra aplicación, en este caso la base de datos. Para iniciarlos se usa el métodoMockitoAnnotations.initMocks.
|
| El método Mockito.verify() permite verificar cuántas veces se ha ejecutado un método de un objeto.
|
| El método Mockito.when().thenReturn() indica qué debe de devolver el método que se indique cuando se ejecute.
|
| Por otra parte se pueden usar arguments matchers para realizar llamadas a métodos mediante ‘comodines’, de forma que los párametros a los mismos no se tengan que definir explícitamente. Por ejemplo Mockito.anyString().




