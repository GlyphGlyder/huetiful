<template>
  <div id="Demo">

    <div class="context" :style="{'background-color': `rgb(${red}, ${green}, ${blue})`}">

      <div class="target"/>

      <huetiful class="huetiful"
        :red="red"
        :green="green"
        :blue="blue"
        @red="changeRed"
        @green="changeGreen"
        @blue="changeBlue"/>

    </div>

    <div class="context" :style="{'background-color': `rgb(${red}, ${green}, ${blue})`}">

      <div class="target" />

      <huetiful class="huetiful"
        mode="row"
        orientation="horizontal"
        :red="red"
        :green="green"
        :blue="blue"
        @color="changeColor"/>

    </div>

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

    changeColor: function(color) {
      this.red = color.red;
      this.blue = color.blue;
      this.green = color.green;
    },

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

<style lang="scss">
body, html {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

.huetiful {
  z-index: 1000;
}

.context {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100vh;
  width: 100%;
  position: relative;
}

.target {
  position: absolute;
  width: 80%;
  height: 80%;
  background-color: #FFF;
}
</style>
