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
    </main>
</template>

<script>

export default {
    name: 'AppMain',
    props: {
        searchInput: String,
        filmsList: Array
    },
}
</script>

<style scoped lang="scss">
    main {
        color: white;
        
        .film-list {
            display: flex;
            flex-wrap: wrap;
            align-items: center;
            gap: 1.5rem;
            list-style: none;

            .film {
                background-color: gray;
                padding: .5rem 1rem;
                border-radius: .5rem;
            }
        }
    }
</style>

