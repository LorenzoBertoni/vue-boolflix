<template>
        <div class="flip-card">
        <div class="flip-card-inner">
            <div class="flip-card-front">
                <h1 v-if="series.poster_path == null">
                    Locandina non disponibile per: 
                    <span>{{series.name}}</span>
                </h1>

                <img 
                :src="'https://image.tmdb.org/t/p/w342' + series.poster_path" 
                :alt="series.name"
                >
            </div>

            <div class="flip-card-back">
                <div class="title">
                    <strong>Titolo:</strong> 
                    {{series.name}}
                </div>

                <div class="original-title">
                    <strong>Titolo originale:</strong> 
                    {{series.original_name}}
                </div>

                <div class="original-language">
                    <strong>Lingua originale:</strong>
                    <span class="fi" :class="'fi-' + series.original_language"></span>
                </div>

                <div class="rating">
                    <strong>Voto:</strong>
                    <i class="fa-solid fa-star"
                    v-for="(rating, index) in getRatings(series.vote_average)" 
                    :key="'a' + index"
                    >
                    </i>

                    <i class="fa-regular fa-star"
                    v-for="(rating, index) in (5 - getRatings(series.vote_average))" 
                    :key="'b' + index"
                    >
                    </i>
                </div>

                <div class="overview">
                    <strong>Trama:</strong>
                    {{series.overview}}
                    <span v-if="series.overview == '' ">Non disponibile</span>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'SingleSerie',
    props: {
        series: Object
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