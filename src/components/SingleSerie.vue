<template>
        <li class="series">
            <strong>Titolo:</strong> {{series.name}}
            
            <div class="poster-wrapper">
                <img 
                :src="'https://image.tmdb.org/t/p/w185' + series.poster_path" 
                :alt="series.name">
            </div>

            <ul class="series-info">
                <li class="info">
                    <strong>Titolo originale:</strong> {{series.original_name}}
                </li>

                <li class="info">
                    <strong>Lingua originale:</strong> {{series.original_language}}
                </li>
                
                <li class="info">
                    <strong>Voto:</strong>

                    <i class="fa-solid fa-star"
                    v-for="(rating, index) in getRatings(series.vote_average)" 
                    :key="'c' + index"
                    >
                    </i>

                    <i class="fa-regular fa-star"
                    v-for="(rating, index) in (5 - getRatings(series.vote_average))" 
                    :key="'d' + index"
                    >
                    </i>
                </li>
            </ul>
    </li>
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