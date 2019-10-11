<template>
  <div class="hue-slider" ref="slider"
    @mousemove="dragColor"
    @mouseup="dragging = false"
    @mouseleave="dragging = false">

    <div class="slider-tracks"
      :style="{'background': gradient}"/>
      
    <div class="knob" ref="knob"
      :style="{
        'left': `${Math.round((color / 255) * 100)}%`
      }"
      @mousedown="dragging = true">
      <div />
    </div>

  </div>
  <!--
  <input type="range" min="0" max="255" step="1"
    v-bind:value="value"
    v-on:input="updateColor($event.target.value)"
    v-bind:class="{'red': color == 'red', 'green': color == 'green', 'blue': color == 'blue'}"/>
  -->
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

  },

  methods: {

    updateColor: function(value) {
      this.$emit('input', value);
    },

    dragColor: function(mouse) {
      if (this.dragging) {

        // Compare delta between mouse position and position of knob.  If the
        // difference is greater than 1/255th the width of the slider, then
        // move
        let knobPos = this.$refs.knob.getBoundingClientRect();
        let delta = mouse.screenX - knobPos.left;

        let sliderPos = this.$refs.slider.getBoundingClientRect();
        if (Math.abs(delta / sliderPos.width) > (1/255)) {
          let colorChange = Math.floor((delta / sliderPos.width) * 128);
          let newColor = this.color + colorChange;
          if (newColor >= 0 && newColor <= 255) {
            this.$emit('color', newColor);
          }
        }
      }
    },

    trackColor: function(count) {

      let color = {
        red: this.channel == 'red' ? count / 70 * 255 : this.wholeColor.red,
        green: this.channel == 'green' ? count / 70 * 255 : this.wholeColor.green,
        blue: this.channel == 'blue' ? count / 70 * 255 : this.wholeColor.blue
      }

      return `rgb(${color.red}, ${color.green}, ${color.blue})`;

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

  &::-webkit-slider-thumb {
    -webkit-appearance: none;
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

/**
 * Thumb Styling
 */
input[type=range] {

  // Webkit
  &::-webkit-slider-thumb {
    -webkit-appearance: none;
    border: 2px solid #555;
    height: 16px;
    width: 16px;
    border-radius: 100%;
    background: #ffffff;
    cursor: pointer;
    margin-top: -5.5px; /* You need to specify a margin in Chrome, but in Firefox and IE it is automatic */
    box-shadow: 0px 1px 1px #AAA; /* Add cool effects to your sliders! */
  }

  // Firefox
  &::-moz-range-thumb {
    box-shadow: 1px 1px 1px #CCC;
    border: 1px solid #CCC;
    height: 16px;
    width: 16px;
    border-radius: 100%;
    background: #ffffff;
    cursor: pointer;
  }

  // IE
  &::-ms-thumb {
    box-shadow: 1px 1px 1px #CCC;
    border: 1px solid #CCC;
    height: 16px;
    width: 16px;
    border-radius: 100%;
    background: #ffffff;
    cursor: pointer;
  }
}

/**
 * Track Styles
 */
input[type=range] {

  // Webkit
  &::-webkit-slider-runnable-track {
    width: 100%;
    max-width: 200px;
    height: 6px;
    cursor: pointer;
    background: #3071a9;
    border-radius: 1.3px;
  }

  &:focus::-webkit-slider-runnable-track {
    background: #FF0000;
  }

  // Firefox
  &::-moz-range-track {
    width: 100%;
    height: 6px;
    cursor: pointer;
    box-shadow: inset 1px 1px 1px #777, 0px 0px 1px #555;
    background: #FFFFF8;
    border-radius: 4px;
  }

  // IE
  &::-ms-track {
    width: 100%;
    height: 8.4px;
    cursor: pointer;
    background: transparent;
    border-color: transparent;
    border-width: 16px 0;
    color: transparent;
  }

  &::-ms-fill-lower {
    background: #2a6495;
    border: 0.2px solid #010101;
    border-radius: 2.6px;
    box-shadow: 1px 1px 1px #000000, 0px 0px 1px #0d0d0d;
  }

  &:focus::-ms-fill-lower {
    background: #3071a9;
  }

  &::-ms-fill-upper {
    background: #3071a9;
    border: 0.2px solid #010101;
    border-radius: 2.6px;
    box-shadow: 1px 1px 1px #000000, 0px 0px 1px #0d0d0d;
  }

  &:focus::-ms-fill-upper {
    background: #367ebd;
  }

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
