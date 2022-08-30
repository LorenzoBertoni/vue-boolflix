<template>
    <header>
        <input 
        type="text" 
        placeholder="Inserisci il titolo del film da cercare"
        v-model="searchInput"
        >

        <button @click="getFilms">Cerca</button>
    </header>
</template>

<script>
import axios from 'axios';

export default {
    name: 'AppHeader',
    data() {
        return {
            filmsList: [],
            searchInput: ''
        }
    },
    methods: {
        getFilms() {
            axios.get('https://api.themoviedb.org/3/search/movie?api_key=3fe6fc37252265374a6f243cf78a5b9f&language=it-IT&query=' + this.searchInput)
            .then(response => {
                this.filmsList = response.data.results;
                this.$emit('searchInput', this.searchInput);
                this.$emit('filmsList', this.filmsList);
            })
            .catch(error => {
                console.log(error);
            })
        }
    }
}
</script>

<style scoped lang="scss">
    header {
        position: sticky;
        top: 0;
        left: 0;
        
        button {
            margin-left: 10px;
        }
    }
</style>