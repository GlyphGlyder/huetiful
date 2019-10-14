<template>
  <div class="hue-slider" ref="slider">

    <input type="range" min="0" max="255" step="1"
      :value="color"
      @input="$emit('color', $event.target.value)"/>

    <div class="slider-tracks"
      :style="{'background': gradient}">
    </div>

  </div>

</template>

<script>
export default {
  name: "HueSlider",
  props: ['channel', 'color', 'value', 'whole-color'],
  data: function() {
    return {
      dragging: false
    }
  },

  computed: {

    // Generates a color gradient from a color with 0 of the color this slider
    // deals with, all the way up to max
    gradient: function() {

      let minColor = {
        red: this.channel == 'red' ? 0 : this.wholeColor.red,
        green: this.channel == 'green' ? 0: this.wholeColor.green,
        blue: this.channel == 'blue' ? 0: this.wholeColor.blue
      };

      let maxColor = {
        red: this.channel == 'red' ? 255 : this.wholeColor.red,
        green: this.channel == 'green' ? 255 : this.wholeColor.green,
        blue: this.channel == 'blue' ? 255 : this.wholeColor.blue
      };

      return `linear-gradient(0.25turn, rgb(${minColor.red}, ${minColor.green}, ${minColor.blue}), rgb(${maxColor.red}, ${maxColor.green}, ${maxColor.blue}))`;

    }

  }

}
</script>

<style lang="scss" scoped>

/**
 * CSS used to hide the input range
 */
input[type=range] {
  -webkit-appearance: none; // Hides the slider so that custom slider can be made
  width: 100%; // Specific width is required for Firefox.
  background: transparent; // Otherwise white in Chrome
  position: absolute;
  z-index: 1000;
  height: 10px;
  margin: 0;
  padding: 0;

  &::-webkit-slider-thumb {
    -webkit-appearance: none;
    display: none;
  }

  // This removes the blue border when focused.  Useful
  &:focus {
    outline: none;
  }

  &::-ms-track {
    width: 100%;
    cursor: pointer;

    // Hides the slider so custom styles can be added
    background: transparent;
    border-color: transparent;
    color: transparent;
  }
}

/* Special styling for WebKit/Blink */
input[type=range]::-webkit-slider-thumb {
  -webkit-appearance: none;
  border: 2px solid #000000;
  height: 16px;
  width: 16px;
  border-radius: 4px;
  background: #ffffff;
  cursor: pointer;
  margin-top: -14px; /* You need to specify a margin in Chrome, but in Firefox and IE it is automatic */
}

/* All the same stuff for Firefox */
input[type=range]::-moz-range-thumb {
  border: 2px solid #000000;
  height: 16px;
  width: 16px;
  border-radius: 4px;
  background: #ffffff;
  cursor: pointer;
}

/* All the same stuff for IE */
input[type=range]::-ms-thumb {
  border: 2px solid #000000;
  height: 16px;
  width: 16px;
  border-radius: 4px;
  background: #ffffff;
  cursor: pointer;
}

.hue-slider {
  width: 100%;
  padding: 6px 0;
  margin: 0px auto;
  position: relative;
}

.slider-tracks {
  position: relative;
  border-radius: 5px;
  //border: 1px solid #BBB;
  height: 10px;

  .gradient {
    position: absolute;
    top: 1px;
    height: 8px;
    left: 1px;
    right: 1px;
    border-radius: 4px;
    background-color: #FFF;
    display: flex;
    align-items: center;
    justify-content: space-around;

    span {
      width: 1px;
      border-left: 1.5px solid #BBB;
      height: 8px;
    }
  }


}

.knob {
  position: absolute;
  left: 50%;
  top: 2px;

  & div {
    position: relative;
    height: 14px;
    width: 14px;
    left: -9px;
    background-color: #FFF;
    border: 2px solid #000;
    border-radius: 4px;
  }
}
</style>
