<template>
    <main>
        <SingleFilm 
        class="film"
        v-for="(film, index) in filmsList" 
        :key="index" 
        :film="film"
        />

        <SingleSerie
        class="series"
        v-for="(serie, index) in tvSeriesList"
        :key="'e' + index"
        :series="serie"
        />
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
        display: flex;
        flex-wrap: wrap;
        justify-content: center;
        gap: 20px;
        margin-top: 2rem;
    }
</style>

