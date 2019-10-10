<!-- Rather than the window, presents a row of different colors, all designed to
 	be changeable -->
<template>
	<div class="hue-row"
		:class="{
			'horizontal': orientation == 'horizontal',
			'vertical': orientation == 'vertical'
		}">

		<HuePaletteWell v-for="color in colors"
			:color="color"
			@setColor="$emit('selected', $event)"/>

	</div>
</template>

<script>
import HuePaletteWell from './HuePaletteWell.vue';
export default {
	name: "HueRow",
	props: ['orientation'],
	components: { HuePaletteWell },
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

	&.horizontal {
		display: flex;
		align-items: center;
	}
}
</style>
