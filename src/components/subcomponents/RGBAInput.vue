<!-- Component for typing in rgba input by hand -->
<template>
	<div>
		<div class="huetiful-rgba">

			<span>
				<strong>R: </strong>
				<input type="text"
					:value="red"
					@input="$emit('red', $event.target.value)">
			</span>

			<span>
				<strong>G: </strong>
				<input type="text"
					:value="green"
					@input="$emit('green', $event.target.value)">
			</span>

			<span>
				<strong>B: </strong>
				<input type="text"
					:value="blue"
					@input="$emit('blue', $event.target.value)">
			</span>

		</div>

		<div class="huetiful-hex">
			<strong>RGB: </strong>
			<input type="text"
				:value="colorHex"
				@input="hexToColor($event.target.value)">
		</div>

	</div>
</template>

<script>
export default {
	name: "RGBAInput",
	props: ['red', 'green', 'blue'],

	computed: {

		// Takes the individual color values passed in as props and converts them
		// into a hex string
		colorHex: function() {
			let red = parseInt(this.red).toString(16).toUpperCase();
			let blue = parseInt(this.blue).toString(16).toUpperCase();
			let green = parseInt(this.green).toString(16).toUpperCase();

			if (red.length < 2) {
				red = "0" + red;
			}
			if (blue.length < 2) {
				blue = "0" + blue;
			}
			if (green.length < 2) {
				green = "0" + green;
			}

			return "#" + red + green + blue;
		}

	},

	methods: {

		// Takes the user's written hex value, attempts to parse it into a color
		// value
		hexToColor: function(value) {

			let red = -1;
			let green = -1;
			let blue = -1;

			let offset = 0;

			for(let i = 0; i < value.length; i ++) {

				let hex = value[i];

				// If it's a sharp symbol, then skip over and set a flag that will
				// offset switch statement below
				if (hex === '#') {
					offset = 1;
					continue;
				}

				// Make sure this is a valid character
				if (hex < '0' || hex > 'F' && hex < 'a' || hex > 'f') {
					return;
				}

				// Check to see if the index is greater than 0 and is odd.  If so, we
				// have enough information to guess a color
				if (i > 0 + offset && i % 2 == 1 - offset) {

					switch (i) {
						case 1 + offset:
							// It's red
							red = parseInt(`${value[i-1]}${value[i]}`, 16)
							break;
						case 3 + offset:
							// It's green
							green = parseInt(`${value[i-1]}${value[i]}`, 16)
							break;
						case 5 + offset:
							// It's blue
							blue = parseInt(`${value[i-1]}${value[i]}`, 16)
							break;
						default:
							// It's a very large number.  Doesn't matter
					}

				}

			}

			// If all of the above colors have been set to values above one, then set
			// our new color value by emitting the individual colors
			if (red >= 0 && green >= 0 && blue >= 0) {
				this.$emit('colors', {red, green, blue});
			}

		}

	}
}
</script>

<style lang="scss" scoped>
.huetiful-rgba {
  display: flex;
  margin: 10px -5px;
	justify-content: center;

  & span {
		width: 0;
		flex-grow: 1;
    margin: 0 5px;
    font-size: 12px;
		display: flex;
		align-items: center;

		&:last-child {
			margin: 0;
		}

		input {
			margin-left: 4px;
			width: 0;
			flex-grow: 1;
		}
  }
}

.huetiful-hex {
	display: flex;
	align-items: center;

	input {
		width: 0;
		flex-grow: 1;
		font-size: 14px;
	}
}

.huetiful-hex input, .huetiful-rgba input {
	border: 1px solid #C1C8E8;
	border-right-color: #A2A8C2;
	border-bottom-color: #A2A8C2;
	border-radius: 3px;
  text-align: center;
	box-shadow: inset 1px 1px 2px rgba(0, 0, 0, 0.2);
	padding: 2px;

	&:focus {
		border-color: #aab4f8;
		box-shadow: inset 1px 1px 1px #aab4f8;
	}
}

.huetiful-rgba input {
	text-align: left;
}
</style>
