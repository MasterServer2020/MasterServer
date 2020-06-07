=========
Servicios
=========

| Los servicios son los encargados de realizar peticiones HTTP usando la librería Axios, cada servicio va a tener acceso a una instancia de axios.

Estructura
==========

1. Servicio

  - api.js
  - playerService.js


Api.js
======

.. code-block:: javascript

		export const axiosInstance = axios.create({
		    baseURL: process.env.VUE_APP_BASE_URL,
		    withCredentials: false,
		    headers: {
		    'Accept': 'application/json',
		    'Content-Type': 'application/json'
		    }
		})


PlayerService.js
================

.. code-block:: javascript

		export default {
		  async retrievePlayersByRank (rankName) {
		    const response = await axiosInstance.get('/players/getByRankName/' + rankName)
		    return response.data
		  },
		  async retrievePlayerByName (name) {
		    var response = {}
		    try {
		      response = await await axiosInstance.get('/player/getByName/' + name)
		    } catch (e) {
		      response = e
		    }
		    return response.data
		  },
		  async retrievePlayersOnlineNumber () {
		    var response = []
		    try {
		      response = await await axiosInstance.get('/players/getByOnline/true')
		    } catch (e) {
		      response = []
		    }
		    return response.data
		  }
		}
