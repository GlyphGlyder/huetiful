<template>
  <input type="range" min="0" max="255" step="1"
    v-bind:value="value"
    v-on:input="updateColor($event.target.value)"
    v-bind:class="{'red': color == 'red', 'green': color == 'green', 'blue': color == 'blue'}"/>
</template>

<script>
export default {
  name: "HueSlider",
  props: ['color', 'value'],

  methods: {

    updateColor: function(value) {
      this.$emit('input', value);
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

</style>
