<!-- Rather than the window, presents a row of different colors, all designed to
 	be changeable -->
<template>
	<div :class="{'has-panel': panel}">

		<div class="hue-row"
			:class="{
				'horizontal': orientation == 'horizontal',
				'vertical': orientation == 'vertical'
			}"
			:style="'panel' ? 'margin-bottom: 10px;' : ''">

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
			:blue="selected.blue"/>
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
	}
}
</script>

<style lang="scss" scoped>
.hue-row {
	border: 2px solid #000;
	border-radius: 4px;
	box-shadow: 2px 2px 2px #BBB;

	&.horizontal{
		display: flex;
		align-items: center;
	}
}

.has-panel {
	display: flex;
	flex-direction: column;
	align-items: stretch;
}
</style>
