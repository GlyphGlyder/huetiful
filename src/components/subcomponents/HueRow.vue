<!-- Rather than the window, presents a row of different colors, all designed to
 	be changeable -->
<template>
	<div :class="{'has-panel': panel, 'horizontal': orientation == 'horizontal'}">

		<div class="hue-row"
			:class="{
				'horizontal': orientation == 'horizontal',
				'vertical': orientation == 'vertical'
			}"
			:style="panelMargin">

			<HuePaletteWell v-for="color in colors"
				:color="color"
				:selected="color == selected"
				@setColor="$emit('selected', $event)"/>

		</div>

		<HuePanel v-if="panel"
			:wide="orientation == 'horizontal' ? true : false"
			:static="true"
			:red="selected.red"
			:green="selected.green"
			:blue="selected.blue"
			@red="handleColor('red', $event)"
			@green="handleColor('green', $event)"
			@blue="handleColor('blue', $event)"/>

	</div>
</template>

<script>
import DefaultRow from '../../mixins/defaultrow.js';
import HuePaletteWell from './HuePaletteWell.vue';
import HuePanel from './HuePanel.vue';
export default {
	name: "HueRow",
	props: ['change-color', 'orientation', 'panel', 'selected'],
	components: { HuePaletteWell, HuePanel },
	mixins: [ DefaultRow ],

	computed: {

		panelMargin: function() {

			if (this.panel && this.orientation == 'horizontal') {
				return 'margin-bottom: 10px;'
			} else if (this.panel) {
				return 'margin-right: 10px;'
			}

			return '';

		}

	},

	methods: {

		// The row comes with a default color palette, but the user can elect to
		// change said colors as they use the panel.  If they've elected to do this,
		// then this function will emit the color event as usual, but also change
		// the selected color
		handleColor: function(channel, value) {


			if (this.changeColor) {

				for(let i = 0; i < this.colors.length; i ++) {

					let channelEquals = this.colors[i].red == this.selected.red &&
						this.colors[i].green == this.selected.green &&
						this.colors[i].blue == this.selected.blue;

					if (channelEquals) {

						this.colors[i][channel] = value;
						break;

					}
				}
			}

			this.$emit(channel, parseInt(value));

		}

	}
}
</script>

<style lang="scss" scoped>
@import '../../styles/style.scss';
.hue-row {
	@include shadow;
	@include standard-borders;
	border-radius: 4px;

	&.horizontal{
		display: flex;
		align-items: center;
	}

	&.vertical {
		display: flex;
		align-items: center;
		flex-direction: column;
	}
}

.has-panel {
	display: flex;
	align-items: stretch;

	&.horizontal {
		flex-direction: column;
	}
}
</style>
