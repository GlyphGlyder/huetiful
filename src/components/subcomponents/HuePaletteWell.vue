<template>
  <div class="hue-palette-well"
    :style="{'background-color': colorRGBA}"
    @click="setColor"/>
</template>

<script>
export default {
  name: "HuePaletteWell",
  props: ['color'],

  computed: {

    /**
     * Returns color as an rgba string
     */
    colorRGBA: function() {
      return "rgba(" + this.color.red + ", " + this.color.green + ", " + this.color.blue + ", " + 100 + ")";
    }

  },

  methods: {

    setColor: function() {
      this.$emit('setColor', this.color);
    }

  }
}
</script>

<style lang="scss" scoped>
.hue-palette-well {
  border-radius: 4px;
  height: 40px;
  width: 40px;
  margin: 4px;
  cursor: pointer;
}
</style>
