<template>
  <div id="app">
    <AppHeader
    @searchInput="getInputFromHeader"
    @filmsList="getFilmsList"
    />

    <AppMain
    :searchInput="headerSearchInput"
    :filmsList="headerFilmsList"
    />

  </div>
</template>

<script>
import AppMain from './components/AppMain.vue';
import AppHeader from './components/AppHeader.vue';

export default {
  name: 'App',
  components: {
    AppMain,
    AppHeader
  },
  data() {
    return {
      headerSearchInput: '',
      headerFilmsList: []
    }
  },
  methods: {
    getInputFromHeader(inputFromHeader) {
      this.headerSearchInput = inputFromHeader;
    },
    getFilmsList(headerFilmsList) {
      this.headerFilmsList = headerFilmsList;
    }
  }
}
</script>

<style lang="scss">

</style>
