<template>
  <v-app>
    <v-content>
      <Search :updateWeatherData="updateWeatherData" />
      <Favorites />
      <Current 
        v-if="Object.keys(weatherData).length > 0"
        :value="dailyTemperatures"
        :dates="dates"
      />
    </v-content>
  </v-app>
</template>

<script>
import Search from './components/Search';
import Current from './components/Current'

export default {
  name: 'App',
  components: {
    Search,
    Current
  },
  data () {
    return {
      weatherData: Object
    }
  },
  methods: {
    updateWeatherData: function(data) {
      this.weatherData = data;
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
