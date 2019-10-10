<!-- Huetiful itself.  Juggles between rendering two components.  The window,
  which is effectively a rounded square, and the panel, which is where all the
  action happens -->
<template>
  <div id="Huetiful">

    <!-- The window is the default option when everythis is minimized.  Shows
      the user what the current color is. -->
    <HueWindow
      v-if="minimized && !mode"
      v-on:click="minimized = false"
      v-bind:minimized="minimized"
      v-bind:red="red"
      v-bind:green="green"
      v-bind:blue="blue"/>

    <HueRow v-if="mode == 'row'"
      :orientation="orientation"
      @selected="$emit('color', $event)"/>

    <hue-panel
      v-if="!minimized && mode != 'row'"
      v-on:close="$emit('close')"
      v-on:minimize="minimize"
      v-on:red="$emit('red', $event)"
      v-on:green="$emit('green', $event)"
      v-on:blue="$emit('blue', $event)"
      v-bind:red="red"
      v-bind:green="green"
      v-bind:blue="blue">
    </hue-panel>

  </div>
</template>

<script>
import HuePanel from './subcomponents/HuePanel.vue';
import HueRow from './subcomponents/HueRow.vue';
import HueWindow from './subcomponents/HueWindow.vue';
export default {
  name: 'Huetiful',
  components: { HuePanel, HueRow, HueWindow },
  props: ['red', 'green', 'blue', 'expand', 'mode', 'orientation'],
  data: function() {
    return {
      minimized: false
    }
  },

  methods: {

    // Handles minimize events, and bubbles them up to parent in case it wants
    // to do anything
    minimize: function() {

      this.minimized = true;
      this.$emit('minimize');

    }

  },

  mounted: function() {
    this.minimized = this.expand ? false : true;
  }
}
</script>

<style lang="scss">
a svg {
  width: 20px;
  height: 20px;
}
</style>
