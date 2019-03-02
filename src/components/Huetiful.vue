<!-- Huetiful itself.  Juggles between rendering two components.  The window,
  which is effectively a rounded square, and the panel, which is where all the
  action happens -->
<template>
  <div id="Huetiful">

    <hue-window
      v-if="minimized"
      v-on:click="minimized = false"
      v-bind:minimized="minimized"
      v-bind:red="red"
      v-bind:green="green"
      v-bind:blue="blue">
    </hue-window>

    <hue-panel
      v-if="!minimized"
      v-on:close="$emit('close')"
      v-on:minimize="minimized = true"
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
import HueWindow from './subcomponents/HueWindow.vue';
export default {
  name: 'Huetiful',
  components: { HuePanel, HueWindow },
  props: ['red', 'green', 'blue'],
  data: function() {
    return {
      minimized: true
    }
  }
}
</script>

<style lang="scss">
a svg {
  width: 20px;
  height: 20px;
}
</style>
