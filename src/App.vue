<template>
  <div id="Demo">
    <huetiful
      v-bind:red="red"
      v-bind:green="green"
      v-bind:blue="blue"
      v-on:red="changeRed"
      v-on:green="changeGreen"
      v-on:blue="changeBlue"/>
  </div>
</template>

<script>
import Huetiful from './components/Huetiful.vue';
export default {
  name: 'Demo',
  components: { Huetiful },
  data: function() {
    return {
      red: 255,
      green: 0,
      blue: 0
    }
  },

  methods: {

    changeRed: function(red) {
      this.red = red;
    },

    changeGreen: function(green) {
      this.green = green;
    },

    changeBlue: function(blue) {
      this.blue = blue;
    }
  }
}
</script>
