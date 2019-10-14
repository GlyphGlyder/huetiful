<template>
  <div
    class="huetiful-window"
    :class="{minimized, bordered}"
    :style="{'background-color': color}"
    @click="$emit('click')">
  </div>
</template>

<script>
export default {
  name: "HueWindow",
  props: ['minimized', 'red', 'green', 'blue'],

  computed: {

    // Computed property, determines if a colored border should be added to
    // help window contrast better against background
    bordered: function() {

      if (this.red > 248 & this.green > 248 & this.blue > 248) {
        return true;
      }
      return false;
    },

    // Defines the color present on the window at a given moment
    color: function() {

      return `rgb(${this.red},${this.green},${this.blue})`;

    }

  }
}
</script>

<style lang="scss" scoped>
.huetiful-window {
  background-color: #FF0000;
  border-radius: 100%;
  border: 1px solid transparent;
  box-shadow: 0 2px 2px #AAA;
  height: 100px;
  width: 100px;
  transition: border 0.4s ease;

  &.minimized {
    border-radius: 8px;
    width: 40px;
    height: 40px;
    cursor: pointer;
  }

  &.bordered {
    border: 1px solid #CCC;
  }
}
</style>
