<template>

  <div id="HuePanel" ref="panel">

    <div class="huetiful-panel" :class="{'wide': wide}">

      <!-- Controls.  They can minimize the panel, remove huetiful from view
        altogether, or ring in a panel for more. -->
      <HuePanelControls v-if="!static && mode != 'full'"
        :palette="palette"
        @close="$emit('close')"
        @minimize="$emit('minimize')"
        @palette="palette = !palette"/>

      <HueWindow
        :red="red"
        :green="green"
        :blue="blue"/>

      <div class="huetiful-sliders">

        <HueSlider
          channel="red"
          :color="red"
          :whole-color="{red, green, blue}"
          @color="$emit('red', $event)"/>

        <HueSlider
          channel="green"
          :color="green"
          :whole-color="{red, green, blue}"
          @color="$emit('green', $event)"/>

        <HueSlider
          channel="blue"
          :color="blue"
          :whole-color="{red, green, blue}"
          @color="$emit('blue', $event)"/>

      </div>

      <RGBAInput
        :red="red"
        :green="green"
        :blue="blue"
        @red="$emit('red', $event)"
        @green="$emit('green', $event)"
        @blue="$emit('blue', $event)"
        @colors="setColor"/>

    </div>

    <HuePalette v-if="palette || mode == 'full'"
      :mode="mode"
      :panel="element"
      :keep="keep"
      @setColor="setColor"/>

  </div>

</template>

<script>
import { createPopper } from '@popperjs/core';
import HuePalette from './HuePalette.vue';
import HuePanelControls from './HuePanelControls.vue';
import HueSlider from './HueSlider.vue';
import HueWindow from './HueWindow.vue';
import RGBAInput from './RGBAInput.vue';
export default {
  name: "HuePanel",
  props: ['red', 'green', 'blue', 'wide', 'mode', 'static', 'keep', 'window'],
  components: {
    HuePalette,
    HuePanelControls,
    HueSlider,
    HueWindow,
    RGBAInput
  },

  data: function() {
    return {
      element: null,
      palette: false,
      popperInstance: null
    }
  },

  methods: {

    setColor: function(color) {
      this.$emit('red', color.red);
      this.$emit('blue', color.blue);
      this.$emit('green', color.green);
    }

  },

  // If keep is true, then we instead render the panel as a popover
  mounted: function() {

    this.element = this.$refs.panel;

    if (this.keep) {

      this.popperInstance = createPopper(this.window.$el, this.$refs.panel, {
        placement: this.keep.placement ? this.keep.placement : 'right-end',
        modifiers: [
          {
            name: 'offset',
            options: {
              offset: [1, 8]
            }
          }
        ]
      });

    }

  }

}
</script>

<style lang="scss" scoped>
@import '../../styles/style.scss';
#HuePanel {
  display: flex;
  align-items: stretch;
  position: relative;
}

.huetiful-panel {
  @include standard-box;
  @include shadow;
  padding: 8px;
  width: 200px;

  .huetiful-window {
    margin: 20px auto;
  }

  &.wide {
    width: 100%;
  }
}

.huetiful-sliders {
  margin: 0 auto;
}
</style>
