======
Modelo
======

| Los modelos son los encargados de asociar la clase y sus atributos con la tabla y sus campos usando anotaciones que aporta la Java Persistance Api (JPA).

.. code-block:: java

			@Entity
			@Table(name = "\"player\"")
			public class PlayerModel {
				@Id
				@GeneratedValue(strategy = GenerationType.IDENTITY)
				@Column(name = "id")
				private long id;

				@Column(name = "uuid", length = 50)
				private String uuid;
				
				@JsonFormat(pattern = "yyyy-MM-dd'T'HH:mm:ss", timezone = "Europe/Madrid")
				@Column(name = "first_login")
				private LocalDateTime firstLogin;

				@Column(name = "time_played")
				private long timePlayed;
				
				@OneToMany(mappedBy = "assasin", fetch = FetchType.EAGER)
				private Set<DeathModel> assasins = new HashSet<>();
				
				@ManyToOne(fetch = FetchType.EAGER)
			    	@JoinColumn(name="rank_id")
				private RankModel rank;
				
				@OneToOne(fetch = FetchType.EAGER)
			   	@JoinColumn(name="command_id")
				@JsonBackReference
				private CommandModel command;
			}

- @Entity: Declara que la clase es una entidad de JPA.
- @Table: Indica la tabla a la cual se asocia la entidad.
- @Id: Indica que el atributo hace la función de clave primaria en la tabla.
- @GeneratedValue: Informa que el atributo es auto-incrementado automáticamente. Debe de ir conjuntamente con la anotación @Id.
- @Column: Informa de la tabla a la cual va asociada el atributo.
- @ManyToMany: Indica que esta tabla pertenece a una relación de muchos a muchos.
- @ManyToOne: Indica que la tabla pertenece a una relación de muchos a uno.
- @OneToMany: Indica que la tabla pertenece a una relación de uno a muchos.
- @OneToMany: Indica que la tabla pertenece a una relación de uno a uno.
- @JoinColumn: Indica el atributo de la relación al que hace referencia.
- @JsonBackReference: Indica la parte de la relación que no se va a Serializar.
- @JsonFormat: Indica el formato de la fecha.

| Usando la anotación @ManyToMany podemos suprimir el modelo correspondiente de la tabla resultante  en una relación de  muchos a muchos. 
|
| Al hacer una relación bidireccional, para que la librería de JSON “Jackson” funcione correctamente, uno de los dos lados de la relación no debe ser serializado, para evitar un problema de recursión infinita.




