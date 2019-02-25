<template>

  <div id="HuePanel">

    <div class="huetiful-panel">

      <a href="#" class="minimize-link" v-on:click.prevent="minimize">
        <ArrowDown/>
      </a>

      <a href="#" class="minimize-link" v-on:click.prevent="close">
        <i class="fa fa-times"></i>
      </a>

      <a href="#" class="palette-link" v-on:click.prevent="openPalette">
        <ArrowRight v-if="!palette"/>
        <ArrowLeft v-else/>
      </a>

      <hue-window
        v-bind:red="red"
        v-bind:green="green"
        v-bind:blue="blue">
      </hue-window>

      <form class="huetiful-sliders">

        <hue-slider v-model="red"></hue-slider>
        <hue-slider v-model="green"></hue-slider>
        <hue-slider v-model="blue"></hue-slider>

        <div class="huetiful-rgba">
          <input type="text" v-model="red">
          <input type="text" v-model="green">
          <input type="text" v-model="blue">
        </div>

        <input
          type="text"
          class="huetiful-hex"
          v-bind:value="colorHex"
          v-on:input="hexToColor($event.target.value)">

      </form>

    </div>

    <transition name="slide">
      <hue-palette v-if="palette"
        v-on:setColor="setColor"></hue-palette>
    </transition>

  </div>

</template>

<script>
import ArrowDown from '../icons/ArrowDown.vue';
import ArrowLeft from '../icons/ArrowLeft.vue';
import ArrowRight from '../icons/ArrowRight.vue';
import HuePalette from './HuePalette.vue';
import HueSlider from './HueSlider.vue';
import HueWindow from './HueWindow.vue';
export default {

  name: "HuePanel",
  props: ['red', 'green', 'blue'],
  components: {
    ArrowDown,
    ArrowLeft,
    ArrowRight,
    HuePalette,
    HueSlider,
    HueWindow
  },

  data: function() {
    return {
      palette: false
    }
  },

  computed: {

    colorHex: function() {
      var red = parseInt(this.red).toString(16).toUpperCase();
      var blue = parseInt(this.blue).toString(16).toUpperCase();
      var green = parseInt(this.green).toString(16).toUpperCase();

      if (red.length < 2) {
        red = "0" + red;
      }
      if (blue.length < 2) {
        blue = "0" + blue;
      }
      if (green.length < 2) {
        green = "0" + green;
      }

      return "#" + red + blue + green;
    },

  },

  methods: {

    /**
     * Emits a close event.  This bubbles all the way on up and out of the
     * component.  From there, it's up to the user to decide what to do with
     * it
     */
    close: function() {
      this.$emit('close');
    },

    hexToColor: function(value) {

    },

    /**
     * Minimizes the panel
     */
    minimize: function() {
      this.$emit('minimize');
    },

    openPalette: function() {
      this.palette = !this.palette
    },

    setColor: function(color) {
      this.red = color.red;
      this.blue = color.blue;
      this.green = color.green;
    }

  },

  watch: {

    red: function(val) {
      this.$emit('red', val);
    },

    green: function(val) {
      this.$emit('green', val);
    },

    blue: function(val) {
      this.$emit('blue', val);
    }

  }


}
</script>

<style lang="scss" scoped>

#HuePanel {
  display: flex;
  align-items: stretch;
}

.huetiful-panel {
  border: 1px solid #CCC;
  border-radius: 10px;
  box-shadow: 0 2px 2px #CCC;
  padding: 10px;
  width: 200px;
  background-color: #FFF;

  .huetiful-window {
    margin: 20px auto;
  }
}

.huetiful-rgba {
  display: flex;
  justify-content: space-between;
  margin: 10px -5px;

  & input {
    width: 33.33%;
    margin: 0 5px;
    font-size: 12px;
  }
}

.huetiful-hex {
  width: 100%;
  font-size: 14px;
}

.huetiful-hex, .huetiful-rgba input {
  border: none;
  border-bottom: 1px solid #DDD;
  text-align: center;
  font-weight: 500;
}

.minimize-link {
  margin: 0 4px;
  float: left;
}

.palette-link {
  margin: 0 4px;
  float: right;
}

.slide-enter, .slide-leave-to {
  left: -150px;
  opacity: 0;
  z-index: -20;
}

.slide-enter-active, .slide-leave-active {
  transition: all 0.25s ease;
}

.slide-enter-to, .slide-leave {
  left: 0;
}

a svg {
  width: 20px;
  height: 20px;
}
</style>
