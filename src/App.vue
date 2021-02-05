<template>
  <div id="Demo">

    <DemoSection :red="red" :green="green" :blue="blue">

      <huetiful class="huetiful"
        :red="red"
        :green="green"
        :blue="blue"
        @red="changeRed"
        @green="changeGreen"
        @blue="changeBlue"/>

    </DemoSection>

    <DemoSection :red="red" :green="green" :blue="blue">

      <!-- This example keeps the window, and renders the panel as a pop-up -->
      <huetiful class="huetiful"
        :red="red"
        :green="green"
        :blue="blue"
        :keep="true"
        :inset="true"
        @red="changeRed"
        @green="changeGreen"
        @blue="changeBlue"/>

    </DemoSection>

    <DemoSection :red="red" :green="green" :blue="blue">

      <huetiful class="huetiful"
        mode="row"
        orientation="horizontal"
        :red="red"
        :green="green"
        :blue="blue"
        @red="changeRed"
        @green="changeGreen"
        @blue="changeBlue"
        @color="changeColor"/>

    </DemoSection>

    <DemoSection :red="red" :green="green" :blue="blue">

      <huetiful class="huetiful"
        mode="row"
        orientation="vertical"
        :red="red"
        :green="green"
        :blue="blue"
        @color="changeColor"/>

    </DemoSection>

    <DemoSection :red="red" :green="green" :blue="blue">

      <huetiful class="huetiful"
        mode="row"
        orientation="horizontal"
        :panel="true"
        :change-color="true"
        :red="red"
        :green="green"
        :blue="blue"
        @red="changeRed"
        @green="changeGreen"
        @blue="changeBlue"
        @color="changeColor"/>

    </DemoSection>

    <DemoSection :red="red" :green="green" :blue="blue">

      <huetiful class="huetiful"
        mode="row"
        orientation="vertical"
        :panel="true"
        :red="red"
        :green="green"
        :blue="blue"
        @red="changeRed"
        @green="changeGreen"
        @blue="changeBlue"
        @color="changeColor"/>

    </DemoSection>

    <DemoSection :red="red" :green="green" :blue="blue">

      <huetiful class="huetiful"
        mode="full"
        orientation="row"
        :red="red"
        :green="green"
        :blue="blue"
        @red="changeRed"
        @green="changeGreen"
        @blue="changeBlue"
        @color="changeColor"/>

    </DemoSection>

  </div>
</template>

<script>
import DemoSection from './components/demo/DemoSection.vue';
import Huetiful from './components/Huetiful.vue';
export default {
  name: 'Demo',
  components: { DemoSection, Huetiful },
  data: function() {
    return {
      red: 255,
      green: 0,
      blue: 0,
      colors: []
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

<style src="./styles/style.scss" lang="scss" />
