<template>
    <div class="flip-card">
        <div class="flip-card-inner">
            <div class="flip-card-front">
                <h1 v-if="film.poster_path == null">
                    Locandina non disponibile per: 
                    <span>{{film.title}}</span>
                </h1>

                <img 
                :src="'https://image.tmdb.org/t/p/w342' + film.poster_path" 
                :alt="film.title"
                >
            </div>

            <div class="flip-card-back">
                <div class="title">
                    <strong>Titolo:</strong> 
                    {{film.title}}
                </div>

                <div class="original-title">
                    <strong>Titolo originale:</strong> 
                    {{film.original_title}}
                </div>

                <div class="original-language">
                    <strong>Lingua originale:</strong>
                    <span class="fi" 
                    :class="(film.original_language == 'en')? 'fi-gb':'fi-' + film.original_language"
                    v-if="film.original_language != 'ja'">
                    </span>

                    <span class="fi" 
                    :class="(film.original_language == 'ja')? 'fi-jp' : '' "
                    v-if="film.original_language == 'ja'">
                    </span>
                </div>

                <div class="rating">
                    <strong>Voto:</strong>
                    <i class="fa-solid fa-star"
                    v-for="(rating, index) in getRatings(film.vote_average)" 
                    :key="'a' + index"
                    >
                    </i>

                    <i class="fa-regular fa-star"
                    v-for="(rating, index) in (5 - getRatings(film.vote_average))" 
                    :key="'b' + index"
                    >
                    </i>
                </div>

                <div class="overview">
                    <strong>Trama:</strong>
                    {{film.overview}}
                    <span v-if="film.overview == '' ">Non disponibile</span>
                </div>
                
                <div class="cast">
                    <strong>Cast:</strong>

                    <span @click="getCast">Vedi cast</span>

                    <ul>
                        <li v-if="cast.length == 0"
                        style="list-style: none;"
                        >
                        </li>
                        <li v-if="cast.length >= 1">{{cast[0].name}}</li>
                        <li v-if="cast.length >= 2">{{cast[1].name}}</li>
                        <li v-if="cast.length >= 3">{{cast[2].name}}</li>
                        <li v-if="cast.length >= 4">{{cast[3].name}}</li>
                        <li v-if="cast.length >= 5">{{cast[4].name}}</li>
                    </ul>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    name: 'SingleFilm',
    props: {
        film: Object
    },
    data() {
        return {
            cast: []
        }
    },
    methods: {
        getRatings(rating) {
            if (rating <= 2) {
                return 1;
            } else if (rating > 2 && rating <= 4) {
                return 2;
            } else if (rating > 4 && rating <= 6) {
                return 3;
            } else if (rating > 6 && rating <= 8) {
                return 4;
            } else if (rating > 8 && rating <= 10) {
                return 5;
            }
        },
        getCast() {
            axios.get('https://api.themoviedb.org/3/movie/' + this.film.id + '/credits?api_key=3fe6fc37252265374a6f243cf78a5b9f&language=it_IT')
            .then(cast => {
                this.cast = cast.data.cast;
            })
        }
    }
}
</script>

<style scoped lang="scss">
    
</style>