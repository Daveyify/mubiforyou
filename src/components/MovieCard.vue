<template>
    <div class="card" @click="$router.push('/movie/' + movie.id)">
        <img :src="poster" :alt="movie.title" class="card-img" />
        <div class="card-info">
            <h3 class="card-title">{{ movie.title }}</h3>
            <div class="card-meta">
                <span class="rating">⭐ {{ movie.vote_average.toFixed(1) }}</span>
                <span class="year">{{ movie.release_date?.slice(0, 4) }}</span>
            </div>
        </div>
    </div>
</template>

<script>
import { IMG_URL } from '../config'

export default {
    name: 'MovieCard',
    props: {
        movie: { type: Object, required: true }
    },
    computed: {
        poster() {
            return this.movie.poster_path
                ? IMG_URL + this.movie.poster_path
                : 'https://via.placeholder.com/300x450?text=Sin+imagen'
        }
    }
}
</script>

<style scoped>
.card {
    background: #030d1f;
    border-radius: 12px;
    overflow: hidden;
    cursor: pointer;
    transition: transform 0.2s, box-shadow 0.2s;
}

.card:hover {
    transform: translateY(-6px);
    box-shadow: 0 8px 24px rgba(58, 255, 101, 0.3);
}

.card-img {
    width: 100%;
    height: 280px;
    object-fit: cover;
}

.card-info {
    padding: 12px;
}

.card-title {
    font-size: 0.95rem;
    margin-bottom: 8px;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
}

.card-meta {
    display: flex;
    justify-content: space-between;
    font-size: 0.85rem;
    color: #aaa;
}

.rating {
    color: #f5c518;
}
</style>