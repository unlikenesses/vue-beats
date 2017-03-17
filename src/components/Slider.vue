<template>
	<div class="bpmRange">
		<div class="bpmTitle">BPM:</div><input type="range" id="bpm" min="1" max="420" step="1" v-model="rangeValue" @change="changeBpm" />
		<output htmlFor="bpm" id="bpmOutput">{{ rangeValue }}</output>
	</div>
</template>

<script>
	export default {
		props: ['bpm'],
		data() {
			return {
				rangeValue: this.bpm
			}
		}, 
		methods: {
			changeBpm() {
				this.$emit('changeBpm', this.rangeValue);
			}
		}
	}
</script>

<style>
	.bpmRange {
		float: right;
	}

	.bpmTitle {
		float: left;
		margin: 7px 8px 0 0;
	}

	#bpm {
		float: left;
	}

	#bpmOutput {
		width: 30px;
		margin: 7px 0 0 8px;
		float: left;
	}
	input[type=range] {
	  width: 16em;
	  -webkit-appearance: none;
	  margin: 16.55px 0;
	}
	input[type=range]:focus {
	  outline: none;
	}
	input[type=range]::-webkit-slider-runnable-track {
	  width: 100%;
	  height: 2.9px;
	  cursor: pointer;
	  box-shadow: 0px 0px 0px #000000, 0px 0px 0px #0d0d0d;
	  background: #606060;
	  border-radius: 20px;
	  border: 0.1px solid #010101;
	}
	input[type=range]::-webkit-slider-thumb {
	  box-shadow: 0.5px 0.5px 11.2px rgba(0, 0, 0, 0.46), 0px 0px 0.5px rgba(13, 13, 13, 0.46);
	  border: 0px solid #000000;
	  height: 36px;
	  width: 16px;
	  border-radius: 3px;
	  background: #ffffff;
	  cursor: pointer;
	  -webkit-appearance: none;
	  margin-top: -16.65px;
	}
	input[type=range]:focus::-webkit-slider-runnable-track {
	  background: #636363;
	}
	input[type=range]::-moz-range-track {
	  width: 100%;
	  height: 2.9px;
	  cursor: pointer;
	  box-shadow: 0px 0px 0px #000000, 0px 0px 0px #0d0d0d;
	  background: #606060;
	  border-radius: 20px;
	  border: 0.1px solid #010101;
	}
	input[type=range]::-moz-range-thumb {
	  box-shadow: 0.5px 0.5px 11.2px rgba(0, 0, 0, 0.46), 0px 0px 0.5px rgba(13, 13, 13, 0.46);
	  border: 0px solid #000000;
	  height: 36px;
	  width: 16px;
	  border-radius: 3px;
	  background: #ffffff;
	  cursor: pointer;
	}
	input[type=range]::-ms-track {
	  width: 100%;
	  height: 2.9px;
	  cursor: pointer;
	  background: transparent;
	  border-color: transparent;
	  color: transparent;
	}
	input[type=range]::-ms-fill-lower {
	  background: #5d5d5d;
	  border: 0.1px solid #010101;
	  border-radius: 40px;
	  box-shadow: 0px 0px 0px #000000, 0px 0px 0px #0d0d0d;
	}
	input[type=range]::-ms-fill-upper {
	  background: #606060;
	  border: 0.1px solid #010101;
	  border-radius: 40px;
	  box-shadow: 0px 0px 0px #000000, 0px 0px 0px #0d0d0d;
	}
	input[type=range]::-ms-thumb {
	  box-shadow: 0.5px 0.5px 11.2px rgba(0, 0, 0, 0.46), 0px 0px 0.5px rgba(13, 13, 13, 0.46);
	  border: 0px solid #000000;
	  height: 36px;
	  width: 16px;
	  border-radius: 3px;
	  background: #ffffff;
	  cursor: pointer;
	  height: 2.9px;
	}
	input[type=range]:focus::-ms-fill-lower {
	  background: #606060;
	}
	input[type=range]:focus::-ms-fill-upper {
	  background: #636363;
	}
</style>