<template>
    <main>
        <ul class="film-list">
            <li v-for="(film, index) in filmsList" :key="index" class="film">
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
                        :key="index"
                        >
                        </i>

                        <i class="fa-regular fa-star"
                        v-for="(rating, index) in (5 - getRatings(film.vote_average))" 
                        :key="index"
                        >
                        </i>
                    </li>
                </ul>
            </li>
        </ul>

        <ul class="tv-series-list">
            <li v-for="(series, index) in tvSeriesList" :key="index" class="series">
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
                        :key="index"
                        >
                        </i>

                        <i class="fa-regular fa-star"
                        v-for="(rating, index) in (5 - getRatings(series.vote_average))" 
                        :key="index"
                        >
                        </i>
                    </li>
                </ul>
            </li>
        </ul>
    </main>
</template>

<script>

export default {
    name: 'AppMain',
    props: {
        searchInput: String,
        filmsList: Array,
        tvSeriesList: Array
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

<style scoped lang="scss">
@import '~@fortawesome/fontawesome-free/css/all.css';

    main {
        color: white;
        
        .film-list, .tv-series-list {
            display: flex;
            flex-wrap: wrap;
            align-items: center;
            gap: 1.5rem;
            list-style: none;

            .film, .series {
                background-color: gray;
                padding: .5rem 1rem;
                border-radius: .5rem;
            }
        }

        .poster-wrapper {
            width: 150px;
            height: 150px;
            border: 1px solid black;
            margin: 0 auto;

            img {
                width: 100%;
                height: 100%;
            }
        }
    }
</style>

