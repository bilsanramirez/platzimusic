<template lang="pug">
 #app
  img(src="./assets/logo.png")
  h1 PlatziMusic
  spinner(v-show="loading")
  select(v-model="selectedCountry")
    option(v-for="pais in paises" v-bind:value="pais.value") {{ pais.name }}
  ul
    artista(v-for="artista in artistas" v-bind:artista="artista" v-bind:key="artista.mbid")
</template>

<script>
import Artista from './components/Artistas';
import Spinner from './components/Spinner';
import getAtistas from './api';

export default {
  name: 'app',
  data () {
    return {
      artistas: [],
      paises: [
        {name: 'Argentina', value: 'argentina'},
        {name: 'Colombia', value: 'colombia'},
        {name: 'España', value: 'spain'},
        {name: 'Honduras', value: 'honduras'}
      ],
      selectedCountry: 'colombia',
      loading: true
    }
  },
  methods: {
    refreshArtists(){
      const self = this;
      this.loading = true;
      this.artistas = [];
      getAtistas(this.selectedCountry).then( function(artistas){
      self.loading = false;
      self.artistas = artistas;
    } );
    }
  },
  watch: {
    selectedCountry: function(){
       this.refreshArtists();
    }
  },
  components: {
    Artista,
    Spinner
  },
  mounted: function(){
    this.refreshArtists();
  }
}
</script>

<style lang="stylus">
#app
	font-family 'Avenir', Helvetica, Arial, sans-serif
	-webkit-font-smoothing antialiased
	-moz-osx-font-smoothing grayscale
	text-align center
	color #2c3e50
	margin-top 60px
h1, h2
	font-weight normal
ul
	list-style-type none
	padding 0
li
	display block
	margin 15px 10px
a
	color #42b983


</style>
