<template>
    <li>
        <strong>Titolo:</strong> {{film.title}}

        <div class="poster-wrapper">
            <img 
            :src="'https://image.tmdb.org/t/p/w185' + film.poster_path" 
            :alt="film.title"
            >
        </div>

        <ul class="film-info">
            <li class="info">
                <strong>Titolo originale:</strong> {{film.original_title}}
            </li>

            <li class="info">
                <strong>Lingua originale:</strong> {{film.original_language}}
            </li>
            
            <li class="info">
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
            </li>
        </ul>
    </li>
</template>

<script>
export default {
    name: 'SingleFilm',
    props: {
        film: Object
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
        }
    }
}
</script>

<style>

</style>