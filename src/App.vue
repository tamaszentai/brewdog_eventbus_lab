<template>
  <div id="app">
    <h1>Brewdog beers</h1>
    <div>
    <beers-list :beers='beers'></beers-list>
    <beer-detail :beer='selectedBeer'></beer-detail>
    <br>
    <h1>Favourite beers</h1>
    <div v-for="(beer, index) in favouriteBeers">{{beer.name}}
      <button @click="removeFavourite(index)">Remove from favourites</button></div>
  </div>
  </div>
</template>

<script>
import BeersList from './components/BeersList.vue';
import BeerDetail from './components/BeerDetail.vue';
import {eventBus} from './main.js';

export default {
  name: 'App',
  data() {
    return {
      beers: [],
      favouriteBeers: [],
      selectedBeer: null,
      favouriteBeer: null
    };
  },
  mounted(){
    fetch('https://api.punkapi.com/v2/beers?page=1&per_page=80')
    .then(res => res.json())
    .then(beers1 => this.beers = [...this.beers, ...beers1])
    fetch('https://api.punkapi.com/v2/beers?page=2&per_page=80')
    .then(res => res.json())
    .then(beers2 => this.beers = [...this.beers, ...beers2])
    fetch('https://api.punkapi.com/v2/beers?page=3&per_page=80')
    .then(res => res.json())
    .then(beers3 => this.beers = [...this.beers, ...beers3])
    fetch('https://api.punkapi.com/v2/beers?page=4&per_page=80')
    .then(res => res.json())
    .then(beers4 => this.beers = [...this.beers, ...beers4])
    fetch('https://api.punkapi.com/v2/beers?page=5&per_page=80')
    .then(res => res.json())
    .then(beers5 => this.beers = [...this.beers, ...beers5])

    eventBus.$on('beer-selected', (beer) => {
      this.selectedBeer = beer;
    });
    eventBus.$on("favourite-beer-added", (favouriteBeer) => {
      if (!this.favouriteBeers.includes(favouriteBeer)) {
        this.favouriteBeers = [...this.favouriteBeers, favouriteBeer];
      }
    });
  },
  components: {
    "beers-list": BeersList,
    "beer-detail": BeerDetail
  },
  methods: {
    removeFavourite: function(index) {
      this.favouriteBeers.splice(index, 1)
    }
}
}

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
