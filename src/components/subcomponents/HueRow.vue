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
			@red="$emit('red', $event)"
			@green="$emit('green', $event)"
			@blue="$emit('blue', $event)"/>
	</div>
</template>

<script>
import HuePaletteWell from './HuePaletteWell.vue';
import HuePanel from './HuePanel.vue';
export default {
	name: "HueRow",
	props: ['orientation', 'panel', 'selected'],
	components: { HuePaletteWell, HuePanel },
	data: function() {
		return {
			colors: [
				{
					red: 255,
					green: 46,
					blue: 0
				},
				{
					red: 255,
					green: 162,
					blue: 39
				},
				{
					red: 255,
					green: 208,
					blue: 0
				},
				{
					red: 0,
					green: 226,
					blue: 64
				},
				{
					red: 35,
					green: 168,
					blue: 252
				},
				{
					red: 109,
					green: 0,
					blue: 255
				}
			]
		}
	},

	computed: {

		panelMargin: function() {

			if (this.panel && this.orientation == 'horizontal') {
				return 'margin-bottom: 10px;'
			} else if (this.panel) {
				return 'margin-right: 10px;'
			}

			return '';

		}

	}
}
</script>

<style lang="scss" scoped>
.hue-row {
	border: 2px solid #000;
	border-radius: 10px;
	box-shadow: 2px 2px 2px #BBB;

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
