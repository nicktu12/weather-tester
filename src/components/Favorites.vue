<template>
  <div class="favorites">
    <v-chip 
      close 
      v-for="(favorite, index) in favorites" 
      :key="index"
      @click="updateWeatherData(weatherData)"
    >
      {{favorite.title}}
    </v-chip>
  </div>
</template>

<script>
export default {
  name: 'favorites',
  props: {
    favorites: Array,
    weatherData: Object,
    updateWeatherData: Function
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
