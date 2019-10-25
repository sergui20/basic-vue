<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <h1>Platzi Music</h1>
    <select v-model="selectedCountry">
      <option v-for="country in countries" v-bind:key="country.value" v-bind:value="country.value">{{ country.name }}</option>
    </select>
    <spinner v-show="loading"></spinner>
    <ul v-if="artists.length > 0">
      <artist v-for="artist in artists" v-bind:artist="artist" v-bind:key="artist.mbid">{{ artist.name }}</artist>
    </ul>
  </div>
</template>

<script>
  import Artist from './components/Artist';
  import getArtists from './api/index';
  import Spinner from './components/Spinner';

  export default {
    name: 'app',
    data() {
      return {
        artists: [],
        countries: [{name: 'Ecuador', value: 'ecuador'}, {name: 'Colombia', value: 'colombia'}, {name: 'Argentina', value: 'argentina'}],
        selectedCountry: 'Ecuador',
        loading: true
      }
    },
    components: {
      Artist,
      Spinner
    },
    methods: {
      fetchArtists(){
        this.loading = true
        this.artists = []
        getArtists(this.selectedCountry)
          .then((artists) => {
            this.loading = false
            this.artists = artists
          })
      }
    },
    mounted() {
      this.fetchArtists()
    },
    watch: {
      selectedCountry() {
        this.fetchArtists()
      }
    }
  }
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
