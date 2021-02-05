<!-- Huetiful itself.  Juggles between rendering two components.  The window,
  which is effectively a rounded square, and the panel, which is where all the
  action happens, albeit you can configure it to keep the window and have the
  panel render to the side -->
<template>
  <div id="Huetiful">

    <!-- The window is the default option when everything is minimized.  Shows
      the user what the current color is. -->
    <HueWindow v-if="minimized && !mode"
      :minimized="minimized"
      :red="red"
      :green="green"
      :blue="blue"
      :keep="keep"
      :inset="inset"
      @click="minimized = false"/>

    <!-- Presents user with a row of up to 6 colors.  Colors can be defined by
      the user, otherwise we supply them. -->
    <HueRow v-if="mode == 'row'"
      :change-color="changeColor"
      :orientation="orientation"
      :panel="panel"
      :selected="{red, green, blue}"
      @selected="$emit('color', $event)"
      @red="$emit('red', $event)"
      @green="$emit('green', $event)"
      @blue="$emit('blue', $event)"/>

    <!-- Default when user expands color picker.  Presents a panel with sliders
      and a palette of colors. -->
    <HuePanel v-if="!minimized && mode != 'row'"
      :red="red"
      :green="green"
      :blue="blue"
      :close="close"
      :mode="mode"
      @close="$emit('close')"
      @minimize="minimize"
      @red="$emit('red', $event)"
      @green="$emit('green', $event)"
      @blue="$emit('blue', $event)" />

  </div>
</template>

<script>
import HuePanel from './subcomponents/HuePanel.vue';
import HueRow from './subcomponents/HueRow.vue';
import HueWindow from './subcomponents/HueWindow.vue';
export default {
  name: 'Huetiful',
  components: { HuePanel, HueRow, HueWindow },
  props: [
    'change-color',
    'colors',
    'red',
    'green',
    'blue',
    'close',
    'expand',
    'mode',
    'orientation',
    'panel'
  ],
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
    this.minimized = this.expand || this.mode == 'full' ? false : true;
  }
}
</script>

<style lang="scss">
a svg {
  width: 20px;
  height: 20px;
}
</style>
