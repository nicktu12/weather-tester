<template>
  <div class="current">
    <v-sparkline
        :fill="true"
        :gradient="['red', 'orange', 'yellow']"
        :line-width="2"
        :padding="0"
        :smooth="6 || false"
        :value="value"
        auto-draw
      ></v-sparkline>
      <v-bottom-nav>
        <span v-for="(date, index) in dates" style="text-align: center;" :key="index">
          {{date}}
        </span>
      </v-bottom-nav>
      <span class="max">{{high}} °F</span>
      <span class="min">{{low}} °F</span>
      <v-btn
        absolute
        dark
        fab
        top
        right
        color="#02A9EA"
      ><v-icon style="font-style: normal;">☆</v-icon></v-btn>
  </div>
</template>

<script>
export default {
  name: 'Current',
  props: {
    value: Array,
    dates: Array
  },
  computed: {
    low: function() {
      return Math.min(...this.value) * 9 / 5 + 32;
    },
    high: function() {
      return Math.max(...this.value) * 9 / 5 + 32;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .current {
    position: relative;
  }

  .current .max {
    position: absolute;
    top: 75px;
    left: 10px;
    font-size: 16px;
  }
  
  .current .min {
    position: absolute;
    bottom: 75px;
    left: 10px;
    font-size: 16px;
  }
</style>
