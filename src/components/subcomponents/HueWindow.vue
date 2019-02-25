<template>
  <div
    id="HueWindow"
    class="huetiful-window"
    v-bind:class="{minimized, bordered}"
    v-bind:style="{'background-color': color}"
    v-on:click="onClick">
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

      if (this.red > 250 & this.green > 250 & this.blue > 250) {
        return true;
      }
      return false;
    },

    // Defines the color present on the window at a given moment
    color: function() {

      return "rgba(" + this.red + "," + this.green + ", " + this.blue + ", " + 100 + ")";

    }

  },

  methods: {

    onClick: function() {
      this.$emit('click');
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
  cursor: pointer;
  height: 100px;
  width: 100px;
  transition: border 0.4s ease;

  &.minimized {
    border-radius: 8px;
    width: 40px;
    height: 40px;
  }

  &.bordered {
    border: 1px solid #CCC;
  }
}
</style>
