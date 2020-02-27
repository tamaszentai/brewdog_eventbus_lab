<template>
  <div id="app">
    <h1>Brewdog beers</h1>
    <div>
    <beers-list :beers='beers'></beers-list>
    <beer-detail :beer='selectedBeer'></beer-detail>
    <br>
    <h1>Favourite beers</h1>
    <div v-for="beer in favouriteBeers">{{beer.name}}</div>
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
    fetch('https://api.punkapi.com/v2/beers')
    .then(res => res.json())
    .then(beers => this.beers = beers)

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
