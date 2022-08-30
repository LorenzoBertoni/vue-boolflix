<template>
    <main>
        <ul class="film-list">
            <li v-for="(film, index) in filmsList" :key="index" class="film">
                <strong>Titolo:</strong> {{film.title}}

                <ul class="film-info">
                    <li class="info">
                        <strong>Titolo originale:</strong> {{film.original_title}}
                    </li>
                    <li class="info">
                        <strong>Lingua originale:</strong> {{film.original_language}}
                    </li>
                    <li class="info">
                        <strong>Voto:</strong> {{film.vote_average}}
                    </li>
                </ul>
            </li>
        </ul>

        <ul class="tv-series-list">
            <li v-for="(series, index) in tvSeriesList" :key="index" class="series">
                <strong>Titolo:</strong> {{series.name}}

                <ul class="series-info">
                    <li class="info">
                        <strong>Titolo originale:</strong> {{series.original_name}}
                    </li>
                    <li class="info">
                        <strong>Lingua originale:</strong> {{series.original_language}}
                    </li>
                    <li class="info">
                        <strong>Voto:</strong> {{series.vote_average}}
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

