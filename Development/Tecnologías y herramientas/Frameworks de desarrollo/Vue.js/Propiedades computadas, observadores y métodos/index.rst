==============================================
Propiedades computadas, observadores y métodos
==============================================

| Se usan para reutilizar código, la principal diferencia entre un método y una propiedad computada es que la propiedad computada se almacena en caché y un método no. Esto significa que la propiedad computada nunca se actualizará porque no es reactiva. Por otro lado, los observadores reaccionan a los cambios de una instancia de Vue.

.. code-block:: html

		<script>
		    export default {
			data(){
			    return {
				message: 'Hey',
				reverseMessage3: ''
			    }
			},
			methods: {
			    reverseMessage1() {
				this.message = this.message.split('').reverse().join('')
			    }
			},
			computed: {
			    reverseMessage2() {
				return this.message.split('').reverse().join('')
			    }
			},
			watch: {
			    reverseMessage3() {
				this.message = this.message.split('').reverse().join('')
			    }
			}
		    }
		</script>

