<template>
    <main>
        <div class="fallback" v-if="(filmsList.length == 0 && tvSeriesList.length == 0)">
            <h1>Scrivi il titolo di un film o di una serie tv per cominciare la ricerca</h1>
        </div>

        <h2 v-if="filmsList.length > 0">Film</h2>

        <section id="films-list">
            <div class="films-wrapper"
            v-for="(film, index) in filmsList" 
            :key="index"
            :class="(genreId != null && !film.genre_ids.includes(genreId))? 'hidden':'' "
            >
                <SingleFilm 
                class="film"
                :film="film"
                v-if="genreId == null || film.genre_ids.includes(genreId)"
                />
            </div>
        </section>

        <h2 v-if="tvSeriesList.length > 0">Serie Tv</h2>

        <section id="series-list">
            <div class="series-wrapper"
            v-for="(serie, index) in tvSeriesList"
            :key="'a' + index"
            :class="(genreId != null && !serie.genre_ids.includes(genreId))? 'hidden':'' "
            >
                <SingleSerie
                class="series"
                :series="serie"
                v-if="genreId == null || serie.genre_ids.includes(genreId)"
                />
            </div>
        </section>
    </main>
</template>

<script>
import SingleFilm from './SingleFilm.vue';
import SingleSerie from './SingleSerie.vue';

export default {
    name: 'AppMain',
    components: {
        SingleFilm,
        SingleSerie
    },
    props: {
        searchInput: String,
        filmsList: Array,
        tvSeriesList: Array,
        genreId: Number
    }
}
</script>

<style scoped lang="scss">

    main {
        color: white;
        margin-top: 2rem;

        .fallback {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            font-size: 1.3rem;
        }

        h2 {
            font-size: 4rem;
            text-align: center;
            margin: 1rem 0;
        }

        #films-list, #series-list {
            display: flex;
            flex-wrap: wrap;
            margin-left: 1rem;
            gap: 20px;
        }

        .films-wrapper, .series-wrapper {
            width: calc(20% - 20px);
        }
    }

    .hidden {
        display: none;
    }
</style>

