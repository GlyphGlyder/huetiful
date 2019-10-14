<!-- Controls at the top of the hue panel -->
<template>
	<div class="hue-panel-controls">
		<a href="#" class="minimize-link"
			@click.prevent="$emit('minimize')">
			<ArrowDown/>
		</a>

		<a href="#" class="minimize-link"
			@click.prevent="$emit('close')">
			<Times/>
		</a>

		<a href="#" class="palette-link"
			@click.prevent="$emit('palette')">
			<ArrowRight v-if="!palette"/>
			<ArrowLeft v-else/>
		</a>
	</div>
</template>

<script>
import ArrowDown from '../icons/ArrowDown.vue';
import ArrowLeft from '../icons/ArrowLeft.vue';
import ArrowRight from '../icons/ArrowRight.vue';
import Times from '../icons/Times.vue';
export default {
	name: "HuePanelControls",
	components: {
		ArrowDown,
		ArrowLeft,
		ArrowRight,
		Times
	},
	props: ['palette']
}
</script>

<style lang="scss" scoped>
.minimize-link {
  margin: 0 4px;
  float: left;
}

.palette-link {
  margin: 0 4px;
  float: right;
}
</style>
