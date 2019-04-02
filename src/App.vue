<template>
  <v-app>
    <v-content>
      <Search :updateWeatherData="updateWeatherData" />
      <Current />
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
      console.log({data})
    }
  }
}
</script>
