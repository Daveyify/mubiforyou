<template>
    <div class="home">
        <h1 class="titulo">{{ buscando ? 'Resultados de búsqueda' : 'PELÍCULAS POPULARES' }}</h1>

        <SearchBar @buscar="buscarPeliculas" @limpiar="cargarPopulares" />

        <!-- Muestra un mensaje mientras carga -->
        <div v-if="cargando" class="loading">Cargando películas... 🎬</div>

        <!-- Muestra error si algo falla -->
        <div v-else-if="error" class="error">{{ error }}</div>

        <!-- Grilla de películas -->
        <div v-else class="grid">
            <MovieCard v-for="pelicula in peliculas" :key="pelicula.id" :movie="pelicula" />
        </div>

        <!-- Sin resultados -->
        <div v-if="!cargando && peliculas.length === 0" class="empty">
            No se encontraron películas 😕
        </div>
    </div>
</template>

<script>
import axios from 'axios'
import { API_KEY, BASE_URL } from '../config'
import MovieCard from '../components/MovieCard.vue'
import SearchBar from '../components/SearchBar.vue'

export default {
    name: 'HomeView',
    components: { MovieCard, SearchBar },
    data() {
        return {
            peliculas: [],   
            cargando: true,  
            error: null,     
            buscando: false  
        }
    },
    mounted() {
        this.cargarPopulares()
    },
    methods: {
        async cargarPopulares() {
            this.cargando = true
            this.buscando = false
            this.error = null
            try {
                const res = await axios.get(`${BASE_URL}/movie/popular`, {
                    params: { api_key: API_KEY, language: 'es-ES', page: 1 }
                })
                this.peliculas = res.data.results
            } catch (e) {
                this.error = 'Error al cargar las películas. Verifica tu API Key.'
            } finally {
                this.cargando = false
            }
        },
        async buscarPeliculas(query) {
            this.cargando = true
            this.buscando = true
            this.error = null
            try {
                const res = await axios.get(`${BASE_URL}/search/movie`, {
                    params: { api_key: API_KEY, language: 'es-ES', query }
                })
                this.peliculas = res.data.results
            } catch (e) {
                this.error = 'Error al buscar películas.'
            } finally {
                this.cargando = false
            }
        }
    }
}
</script>

<style scoped>
.home {
    max-width: 1200px;
    margin: 0 auto;
    padding: 32px 16px;
}

.titulo {
    text-align: center;
    font-size: 1.8rem;
    margin-bottom: 8px;
    color: #1150b6;
    font-family: "Boldonse", system-ui;
    font-weight: 400;
    font-style: normal
}

.grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(180px, 1fr));
    gap: 20px;
}

.loading,
.error,
.empty {
    text-align: center;
    padding: 48px;
    font-size: 1.2rem;
    color: #aaa;
}

.error {
    color: #e50914;
}
</style>