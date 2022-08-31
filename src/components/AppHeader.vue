<template>
    <header>
        <div class="logo-wrapper">
            <a href="#" class="logo">
                BOOLFLIX
            </a>
        </div>
        <div class="search-bar-wrapper">
            <input 
            type="text"
            class="search-bar" 
            placeholder="Cerca un film o serie TV"
            v-model="searchInput"
            @input="getLists">

        </div>
    </header>
</template>

<script>
import axios from 'axios';

export default {
    name: 'AppHeader',
    data() {
        return {
            filmsList: [],
            tvSeriesList: [],
            searchInput: ''
        }
    },
    methods: {
        getLists() {
            if(!this.searchInput == '') {
                axios.get('https://api.themoviedb.org/3/search/movie?api_key=3fe6fc37252265374a6f243cf78a5b9f&language=it-IT&query=' + this.searchInput)
                .then(response => {
                    this.filmsList = response.data.results;
                    this.$emit('searchInput', this.searchInput);
                    this.$emit('filmsList', this.filmsList);
                })
                .catch(error => {
                    console.log(error);
                })

                axios.get('https://api.themoviedb.org/3/search/tv?api_key=3fe6fc37252265374a6f243cf78a5b9f&language=it-IT&query=' +
                this.searchInput)
                .then(res => {
                    this.tvSeriesList = res.data.results;
                    this.$emit('tvSeriesList', this.tvSeriesList);
                })
                .catch(err => {
                    console.log(err);
                })
            }
        }
    }
}
</script>

<style scoped lang="scss">
    header {
        background-color: #000;
        padding: 1rem;
        display: flex;
        justify-content: space-between;
        align-items: center;

        .logo-wrapper {
            .logo {
                font-size: 2rem;
                color: red;
                text-decoration: none;

            }
        }

        .search-bar-wrapper {
            .search-bar {
                padding: .5rem 3rem;
            }
        }
        
        button {
            margin-left: 10px;
        }
    }
</style>