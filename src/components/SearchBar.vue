<template>
    <div class="search-container">
        <input v-model="query" @keyup.enter="buscar" type="text" placeholder="Buscar película..."
            class="search-input" />
        <button @click="buscar" class="search-btn">Buscar</button>
        <button v-if="query" @click="limpiar" class="clear-btn">✕Limpiar</button>
    </div>
</template>

<script>
export default {
    name: 'SearchBar',
    emits: ['buscar', 'limpiar'],
    data() {
        return { query: '' }
    },
    methods: {
        buscar() {
            if (this.query.trim()) {
                this.$emit('buscar', this.query)
            }
        },
        limpiar() {
            this.query = ''
            this.$emit('limpiar')
        }
    }
}
</script>

<style scoped>
.search-container {
    display: flex;
    gap: 8px;
    justify-content: center;
    flex-wrap: wrap;
    margin: 24px 0;
}

.search-input {
    padding: 10px 16px;
    border-radius: 8px;
    border: none;
    width: 320px;
    font-size: 1rem;
    background: #6d6d6d88;
    color: white;                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             
    border: 1px solid #333;
}

.search-btn {
    padding: 10px 20px;
    background: #0e99d0;
    color: white;
    border: none;
    border-radius: 8px;
    cursor: pointer;
    font-size: 1rem;
}

.clear-btn {
    padding: 10px 20px;
    background: #333;
    color: white;
    border: none;
    border-radius: 8px;
    cursor: pointer;
}

@media (max-width: 600px) {
    .search-input {
        width: 100%;
    }
}
</style>