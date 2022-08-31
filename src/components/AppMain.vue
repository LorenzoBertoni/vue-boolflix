//todo ****Milestone 4, 5, 6****
<template>
    <main>
        <ul class="film-list">
            <SingleFilm 
            class="film"
            v-for="(film, index) in filmsList" 
            :key="index" 
            :film="film"/>
        </ul>

        <ul class="tv-series-list">
            <SingleSerie
            class="series"
            v-for="(serie, index) in tvSeriesList"
            :key="index"
            :series="serie"/>
        </ul>
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
        tvSeriesList: Array
    }
}
</script>

<style scoped lang="scss">

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
    }
</style>

