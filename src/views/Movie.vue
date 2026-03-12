<template>
    <div class="detail-page">
        <button @click="$router.back()" class="back-btn">← Volver</button>

        <div v-if="cargando" class="loading">Cargando... 🎬</div>

        <div v-else-if="pelicula" class="detail">
            <img :src="poster" :alt="pelicula.title" class="detail-img" />
            <div class="detail-info">
                <h1>{{ pelicula.title }}</h1>
                <p class="tagline">{{ pelicula.tagline }}</p>
                <div class="badges">
                    <span class="badge">⭐ {{ pelicula.vote_average?.toFixed(1) }}</span>
                    <span class="badge">📅 {{ pelicula.release_date?.slice(0, 4) }}</span>
                    <span class="badge">⏱ {{ pelicula.runtime }} min</span>
                </div>
                <p class="overview">{{ pelicula.overview || 'Sin descripción disponible.' }}</p>
                <div class="genres">
                    <span v-for="g in pelicula.genres" :key="g.id" class="genre-tag">{{ g.name }}</span>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios'
import { API_KEY, BASE_URL, IMG_URL } from '../config'

export default {
    name: 'MovieDetail',
    data() {
        return { pelicula: null, cargando: true }
    },
    computed: {
        poster() {
            return this.pelicula?.poster_path
                ? IMG_URL + this.pelicula.poster_path
                : 'https://via.placeholder.com/300x450?text=Sin+imagen'
        }
    },
    mounted() {
        // this.$route.params.id obtiene el ID de la URL (/movie/123)
        this.cargarDetalle(this.$route.params.id)
    },
    methods: {
        async cargarDetalle(id) {
            try {
                const res = await axios.get(`${BASE_URL}/movie/${id}`, {
                    params: { api_key: API_KEY, language: 'es-ES' }
                })
                this.pelicula = res.data
            } catch (e) {
                console.error(e)
            } finally {
                this.cargando = false
            }
        }
    }
}
</script>

<style scoped>
.detail-page {
    max-width: 1000px;
    margin: 0 auto;
    padding: 32px 16px;
}

.back-btn {
    background: #333;
    color: white;
    border: none;
    padding: 8px 16px;
    border-radius: 8px;
    cursor: pointer;
    margin-bottom: 24px;
    font-size: 1rem;
}

.detail {
    display: flex;
    gap: 32px;
    flex-wrap: wrap;
    /* En móvil se apilan verticalmente */
}

.detail-img {
    width: 280px;
    border-radius: 12px;
    flex-shrink: 0;
}

.detail-info {
    flex: 1;
    min-width: 200px;
}

h1 {
    font-size: 2rem;
    margin-bottom: 8px;
}

.tagline {
    color: #aaa;
    font-style: italic;
    margin-bottom: 16px;
}

.badges {
    display: flex;
    gap: 12px;
    margin-bottom: 16px;
    flex-wrap: wrap;
}

.badge {
    background: #1e1e1e;
    padding: 6px 12px;
    border-radius: 20px;
    font-size: 0.9rem;
}

.overview {
    line-height: 1.7;
    color: #ccc;
    margin-bottom: 20px;
}

.genres {
    display: flex;
    gap: 8px;
    flex-wrap: wrap;
}

.genre-tag {
    background: #e50914;
    padding: 4px 12px;
    border-radius: 20px;
    font-size: 0.85rem;
}

@media (max-width: 600px) {
    .detail-img {
        width: 100%;
    }

    h1 {
        font-size: 1.4rem;
    }
}
</style>