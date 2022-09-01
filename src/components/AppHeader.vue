<template>
    <header>
        <div class="logo-wrapper">
            <a href="#" class="logo">
                BOOLFLIX
            </a>
        </div>
        <div class="search-wrapper">
            <input 
            type="text"
            class="search-bar" 
            placeholder="Cerca un film o serie TV"
            v-model="searchInput"
            @input="getLists">

            <select 
            name="genres" 
            id="genres"
            v-model="selectedGenre"
            @change="$emit('genreId', selectedGenre)"
            >
                <option :value="null">Tutti i generi</option>
                <option 
                v-for="(genre, index) in genreList"
                :key="index"
                :value="genre.id"
                >
                {{genre.name}}</option>
            </select>
        </div>
    </header>
</template>

<script>
import axios from 'axios';

export default {
    name: 'AppHeader',
    data() {
        return {
            ApiUrl: 'https://api.themoviedb.org/3',
            filmsList: [],
            tvSeriesList: [],
            genreList: [],
            searchInput: '',
            selectedGenre: null,
        }
    },
    methods: {
        getLists() {
            if(!this.searchInput == '') {

                const paramsObj = {
                    params: {
                            api_key: '3fe6fc37252265374a6f243cf78a5b9f',
                            language: 'it-IT',
                            query: this.searchInput
                        }
                }

                //**Film**
                axios.get(this.ApiUrl + '/search/movie', paramsObj)
                .then(response => {
                    this.filmsList = response.data.results;
                    this.$emit('searchInput', this.searchInput);
                    this.$emit('filmsList', this.filmsList);
                })
                .catch(error => {
                    console.log(error);
                })

                //**serie TV**
                axios.get(this.ApiUrl + '/search/tv', paramsObj)
                .then(res => {
                    this.tvSeriesList = res.data.results;
                    this.$emit('tvSeriesList', this.tvSeriesList);
                })
                .catch(err => {
                    console.log(err);
                })
            }
        },
        getGenres() {
            axios.get(this.ApiUrl + '/genre/movie/list?api_key=3fe6fc37252265374a6f243cf78a5b9f&language=it_IT')
            .then(resp => {
                this.genreList = resp.data.genres;
            })
        }
    },
    mounted() {
        this.getGenres();
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

        .search-wrapper {
            .search-bar, #genres {
                padding: .5rem 3rem;
                margin: 0 .5rem;
                font-size: 1rem;
                font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
            }
        }
        
        button {
            margin-left: 10px;
        }
    }
</style>