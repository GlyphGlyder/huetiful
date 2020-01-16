<template>
  <div id="HuePalette" class="hue-palette" :class="{'mode-full': mode == 'full'}">

    <div>
      <hue-palette-well v-for="color in colors.setOne"
        v-bind:color="color"
        v-on:setColor="setColor">
      </hue-palette-well>
    </div>

    <div>
      <hue-palette-well v-for="color in colors.setTwo"
        v-bind:color="color"
        v-on:setColor="setColor">
      </hue-palette-well>
    </div>

    <div>
      <hue-palette-well v-for="color in colors.setThree"
        v-bind:color="color"
        v-on:setColor="setColor">
      </hue-palette-well>
    </div>

    <div>
      <hue-palette-well v-for="color in colors.setFour"
        v-bind:color="color"
        v-on:setColor="setColor">
      </hue-palette-well>
    </div>

    <div>
      <hue-palette-well v-for="color in colors.setFive"
        v-bind:color="color"
        v-on:setColor="setColor">
      </hue-palette-well>
    </div>

    <div>
      <hue-palette-well v-for="color in colors.setSix"
        v-bind:color="color"
        v-on:setColor="setColor">
      </hue-palette-well>
    </div>

  </div>
</template>

<script>
import HuePaletteWell from './HuePaletteWell.vue';
export default {
  name: "HuePalette",
  components: { HuePaletteWell },
  props: ['mode'],

  data: function() {
    return {
      colors: {
        setOne: [
          {
            red: 255,
            green: 122,
            blue: 92
          },
          {
            red: 255,
            green: 84,
            blue: 46,
          },
          {
            red: 255,
            green: 46,
            blue: 0
          },
          {
            red: 209,
            green: 38,
            blue: 0
          },
          {
            red: 163,
            green: 30,
            blue: 0
          }
        ],
        setTwo: [
          {
            red: 255,
            green: 195,
            blue: 117
          },
          {
            red: 255,
            green: 178,
            blue: 78
          },
          {
            red: 255,
            green: 162,
            blue: 39
          },
          {
            red: 209,
            green: 133,
            blue: 32
          },
          {
            red: 163,
            green: 104,
            blue: 25
          }
        ],
        setThree: [
          {
            red: 255,
            green: 225,
            blue: 92
          },
          {
            red: 255,
            green: 216,
            blue: 46
          },
          {
            red: 255,
            green: 208,
            blue: 0
          },
          {
            red: 209,
            green: 171,
            blue: 0,
          },
          {
            red: 163,
            green: 133,
            blue: 0
          }
        ],
        setFour: [
          {
            red: 92,
            green: 236,
            blue: 133
          },
          {
            red: 46,
            green: 231,
            blue: 98
          },
          {
            red: 0,
            green: 226,
            blue: 64
          },
          {
            red: 0,
            green: 185,
            blue: 53
          },
          {
            red: 0,
            green: 144,
            blue: 41
          }
        ],
        setFive: [
          {
            red: 115,
            green: 199,
            blue: 253
          },
          {
            red: 75,
            green: 183,
            blue: 252
          },
          {
            red: 35,
            green: 168,
            blue: 252
          },
          {
            red: 29,
            green: 138,
            blue: 207
          },
          {
            red: 23,
            green: 107,
            blue: 161
          }
        ],
        setSix: [
          {
            red: 162,
            green: 92,
            blue: 255
          },
          {
            red: 135,
            green: 46,
            blue: 255
          },
          {
            red: 109,
            green: 0,
            blue: 255
          },
          {
            red: 90,
            green: 0,
            blue: 209
          },
          {
            red: 70,
            green: 0,
            blue: 163
          }
        ]
      }
    }
  },

  methods: {

    setColor: function(color) {
      this.$emit('setColor', color);
    }

  }
}
</script>

<style lang="scss" scoped>
.hue-palette {
  position: absolute;
  left: 240px;
  top: 0;
  bottom: 0;
  border: 2px solid #333;
  border-radius: 10px;
  box-shadow:
    0 0 1px #BBB,
    2px 2px 2px #BBB;
  padding: 10px;
  background-color: #FFF;
  width: 288px;

  &.mode-full {
    position: static;
    margin-left: 10px;
  }

  & > div {
    display: inline-flex;
    flex-direction: column;
    justify-content: space-around;
    height: 100%;
  }
}
</style>
