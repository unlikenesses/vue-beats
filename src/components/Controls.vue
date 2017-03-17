<template>
	<div class="controls">
		<a href="#" class="button" @click.prevent="togglePlay">{{playButtonText}}</a> 
		<a href="#" class="button" @click.prevent="clearPattern">Clear Pattern</a> 
		<Slider :bpm="bpm" @changeBpm="changeBpm" />
	</div>
</template>

<script>
	import Slider from './Slider.vue';

	export default {
		props: ['playing', 'bpm'],
		components: { Slider },
		computed: {
			playButtonText() {
				return (this.playing) ? 'Stop' : 'Play';
			}
		},
		methods: {
			togglePlay() {
				this.$emit('togglePlay');
			},
			clearPattern() {
				this.$emit('clearPattern');
			},
			changeBpm(bpm) {
				this.$emit('changeBpm', bpm);
			}
		}
	}
</script>

<style>
	.controls {
		margin: 20px 0 20px 0;
	}
	.button {
	  text-decoration: none;
	  border-radius: 10px;
	  border: none;
	  cursor: pointer;
	  padding: 12px 40px;
	  letter-spacing: 1px;
	  display: inline-block;
	  outline: none;
	  position: relative;
	  background: #D33515;
	  color: #fff;
	  box-shadow: 0 6px #AC210E;
	  margin-right: 10px;
	}

	.button:hover {
	  box-shadow: 0 4px #AC210E;
	  top: 2px;
	}

	.button:active {
	  box-shadow: 0 0 #AC210E;
	  top: 6px;
	}
</style>