<template>
    <v-container>
      <v-layout
        text-xs-center
        wrap
      >
        <v-flex xs12>
          <v-input>
            <slot>
              <v-text-field v-model="city"
                label="Find your city for up to date weather"
              ></v-text-field>
            </slot>
          </v-input>
          <v-btn @click="searchCity">Search</v-btn>
        </v-flex>
      </v-layout>
    </v-container>
</template>

<script>
export default {
  name: 'Search',
  props: {
    msg: String,
    updateWeatherData: Function
  },
  data: function() {
    return {
      city: ""
    }
  },
  methods: {
    searchCity: function() {
      fetch(`https://api.codetabs.com/v1/proxy?quest=https://www.metaweather.com/api/location/search/?query=${this.city}`)
        .then(res => res.json())
        .then(res => {
          let woeid = res[0].woeid;
          fetch(`https://api.codetabs.com/v1/proxy?quest=https://www.metaweather.com/api/location/${woeid}`)
            .then(res => res.json())
            .then(res => { this.updateWeatherData(res) })
            .catch(error => { throw error; })
          })
        .catch(error => { throw error; })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
