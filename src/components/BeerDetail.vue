<template lang="html">
  <div v-if="beer">
    <h3>{{beer.name}}</h3>
    <button @click="addToFavourites">Add to favourites</button>
    <p>Description: {{beer.description}}</p>
    <p>Alcohol by volume: {{beer.abv}}</p>
    <p>First brewed: {{beer.first_brewed}}</p>
    <img :src="beer.image_url">
  </div>
</template>

<script>
import {eventBus} from '../main.js'
export default {
  name: 'beer-detail',
  props: ['beer'],
  methods: {
    addToFavourites() {
      eventBus.$emit("favourite-beer-added", this.beer);
    }
  }
}
</script>

<style lang="css" scoped>
  img {
    height: 15em;
    width: auto;
  }
</style>
