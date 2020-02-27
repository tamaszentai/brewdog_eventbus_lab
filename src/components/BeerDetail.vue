<template lang="html">
  <div v-if="beer">
    <h3>{{beer.name}}</h3>
    <p>Description: {{beer.description}}</p>
    <p>Alcohol by volume: {{beer.abv}}</p>
    <p>First brewed: {{beer.first_brewed}}</p>
    <img :src="beer.image_url">
  </div>
</template>

<script>
export default {
  name: 'beer-detail',
  props: ['beer']
}
</script>

<style lang="css" scoped>
  img {
    height: 15em;
    width: auto;
  }
</style>
