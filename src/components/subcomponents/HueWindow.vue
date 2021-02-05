<template>

  <div
    class="huetiful-window"
    :class="{minimized, bordered, inset}"
    :style="{'background-color': color}"
    @click="$emit('click')"/>

</template>

<script>
export default {
  name: "HueWindow",
  props: ['minimized', 'inset', 'keep', 'red', 'green', 'blue'],

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
@import '../../styles/style.scss';
.huetiful-window {
  background-color: #FF0000;
  border-radius: 100%;
  border: 1px solid transparent;
  height: 100px;
  width: 100px;
  @include shadow;
  transition: border 0.4s ease;

  &.minimized {
    border-radius: 8px;
    width: 40px;
    height: 40px;
    cursor: pointer;
  }

  &.inset {
    box-shadow: inset 1px 1px 2px rgba(0, 0, 0, 0.2);
  }

  &.bordered {
    border: 1px solid #CCC;
  }
}
</style>
