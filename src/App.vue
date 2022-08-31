<template>
  <div id="app">
    <AppHeader
    @searchInput="getInputFromHeader"
    @filmsList="getFilmsList"
    @tvSeriesList="getTvSeriesList"
    />

    <AppMain
    :searchInput="headerSearchInput"
    :filmsList="headerFilmsList"
    :tvSeriesList="headerSeriesList"
    />
  </div>
</template>

<script>
import AppMain from './components/AppMain.vue';
import AppHeader from './components/AppHeader.vue';
import "/node_modules/flag-icons/css/flag-icons.min.css";

export default {
  name: 'App',
  components: {
    AppMain,
    AppHeader
  },
  data() {
    return {
      headerSearchInput: '',
      headerFilmsList: [],
      headerSeriesList: []
    }
  },
  methods: {
    getInputFromHeader(inputFromHeader) {
      this.headerSearchInput = inputFromHeader;
    },
    getFilmsList(headerFilmsList) {
      this.headerFilmsList = headerFilmsList;
    },
    getTvSeriesList(headerSeriesList) {
      this.headerSeriesList = headerSeriesList;
    }
  }
}
</script>

<style lang="scss">
@import '~@fortawesome/fontawesome-free/css/all.css';
@import './styles/general.scss';
@import './styles/singleComponents.scss';

body {
  background-color: gray;
}
</style>
