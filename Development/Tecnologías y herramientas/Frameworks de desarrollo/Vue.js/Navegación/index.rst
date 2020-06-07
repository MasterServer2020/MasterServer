==========
Navegación
==========

| Para poder crear una SPA se necesita de un sistema de rutas. Para esto se va a usar la librería vue-router, que permite crear rutas modulares, haciendo que cada ruta sea un componente.

.. code-block:: javascript

		const router = new Router({
		    mode: 'history',
		    base: process.env.BASE_URL,
		    routes: [
			{
			    path: '*',
			    redirect: '/',
			},
			{
			    path: '/',
			    name: 'home',
			    component: () => import('../views/Home.vue'),
			    meta: {
				title: 'Home'
			    }
			},
			{
			    path: '/players',
			    name: 'players',
			    component: () => import('../views/PlayersView.vue'),
			    meta: {
				title: 'Players'
			    }
			},
			{
			    path: '/players/player/:name',
			    name: 'player',
			    component: () => import('../views/PlayerView.vue'),
			    meta: {
				title: 'Player'
			    }
			}
		    ]
		})

		router.beforeEach((to, from, next) => {
		    if (to.name == 'player') {
			document.title = to.params.name
		    } else {
			document.title = to.meta.title
		    }
		    next()
		})

		export default router

- Mode: Activa el history mode de HTML 5, además evita que aparezca una almohadilla en la url al navegar.
- Base: Usa la url base de la app.
- Routes: Contiene las rutas.
- Redirect: Reemplaza la url actual por la que se indique.
- Path: Ruta a dónde se va a dirigir. Cuando una ruta incluye “:” indica que se le va a pasar un parámetro al componente que se va a asociar.
- Name: Es el nombre que se va a asignar a la ruta.
- Component: Es el componente que se va a asociar a la ruta.

Formas de realizar la navegación
================================

| Para mostrar el contenido de la página actual, se tiene que usar el elemento <router-view>.Permite renderizar componentes dinámicos en base a una url.

.. code-block:: html

			<router-view/>
			
| La navegación se puede realizar de dos formas: al usar un elemento html, o al usar la instancia del router.
|
| Usando un elemento html se usa la directiva “v-bind:to” dónde se tiene que indicar el nombre de la ruta.

-----------------------
Usando un elemento html
-----------------------

.. code-block:: html

		<b-navbar-nav>
		    <b-nav-item :to="{name: 'dashboard'}">Dashboard</b-nav-item>
		 </b-navbar-nav>

----------------
Haciendo un push
----------------

.. code-block:: javascript

			this.router.push({ name: 'player'})








