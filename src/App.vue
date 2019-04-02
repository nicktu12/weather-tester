<template>
  <v-app>
    <v-content>
      <Search :updateWeatherData="updateWeatherData" />
      <Favorites 
        v-if="favorites.length > 0"
        :favorites="favorites"
        :updateWeatherData="updateWeatherData"
        :weatherData="weatherData"
      />
      <Current 
        v-if="Object.keys(weatherData).length > 0"
        :value="dailyTemperatures"
        :dates="dates"
        :addToFavorites="addToFavorites"
        :weatherData="weatherData"
      />
    </v-content>
  </v-app>
</template>

<script>
import Search from './components/Search';
import Current from './components/Current';
import Favorites from './components/Favorites'

export default {
  name: 'App',
  components: {
    Search,
    Current,
    Favorites
  },
  data () {
    return {
      weatherData: Object,
      favorites: []
    }
  },
  methods: {
    updateWeatherData: function(data) {
      this.weatherData = data;
    },
    addToFavorites: function(data) {
      console.log(this.favorites)
      this.favorites.push(data)
    }
  },
  computed: {
    dailyTemperatures: function() {
      return this.weatherData.consolidated_weather.map(day => parseInt(day.the_temp.toFixed(2)));
    },
    dates: function() {
      return this.weatherData.consolidated_weather.map(day => day.applicable_date);
    }
  }
}
</script>
