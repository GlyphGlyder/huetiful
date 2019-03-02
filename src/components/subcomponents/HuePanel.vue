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

      <HueWindow
        v-bind:red="red"
        v-bind:green="green"
        v-bind:blue="blue"/>

      <div class="huetiful-sliders">

        <hue-slider color="red" v-on:input="$emit('red', $event)"/>
        <hue-slider color="green" v-on:input="$emit('green', $event)"/>
        <hue-slider color="blue" v-on:input="$emit('blue', $event)"/>

      </div>

      <RGBAInput
        v-bind:red="red" v-on:red="$emit('red', $event)"
        v-bind:green="green" v-on:green="$emit('green', $event)"
        v-bind:blue="blue" v-on:blue="$emit('blue', $event)"
        v-on:colors="setColor"/>

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
import RGBAInput from './RGBAInput.vue';
export default {

  name: "HuePanel",
  props: ['red', 'green', 'blue'],
  components: {
    ArrowDown,
    ArrowLeft,
    ArrowRight,
    HuePalette,
    HueSlider,
    HueWindow,
    RGBAInput
  },

  data: function() {
    return {
      palette: false
    }
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
      this.$emit('red', color.red);
      this.$emit('blue', color.blue);
      this.$emit('green', color.green);
    }

  },

  /*
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
  */

}
</script>

<style lang="scss" scoped>

#HuePanel {
  display: flex;
  align-items: stretch;
}

.huetiful-panel {
  background-color: #FFF;
  border: 2px solid #333;
  border-radius: 10px;
  box-shadow:
    0 0 1px #BBB,
    2px 2px 2px #BBB;
  padding: 10px;
  width: 200px;

  .huetiful-window {
    margin: 20px auto;
  }
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
</style>
