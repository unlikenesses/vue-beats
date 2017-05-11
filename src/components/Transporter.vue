<template>
	<div class="transporterContainer">
		<TransporterBlank/>
		<TransporterBlank/>
		<TransporterBlank/>
		<TransporterBlank/>
		<TransporterBlank/>
		<TransporterBlank/>
		<TransporterBlank/>
		<TransporterBlank/>
		<div class="transporter">					
			<div class="transportLight transportLightActive" :style="lightPos"></div>
		</div>
	</div>
</template>

<script>
	import TransporterBlank from './TransporterBlank.vue';

	export default {
		props: ['pos'],
		components: { TransporterBlank },
		computed: {
			lightPos() {
				return 'left:' + this.pos * 100 + 'px';
			}
		}
	}
</script>

<style>
	.transporterContainer {
		width: 910px;
		height: 50px;
		border: 1px solid #666;
		background: #333;
		position: absolute;
		bottom: -52px;
	}

	.transporter {
		width: 80px;
		height: 50px;
		margin: 10px 0 0 10px;
		text-align: center;
		left: 0;
		z-index: 1;
		position: absolute;
	}

	.transporterOff {
		width: 100px;
		height: 60px;
		margin: 10px 0 0 0;
		text-align: center;
		float: left;
	}

	.transportLight {
		border-radius: 50%;
		background-color: #001100;
		width: 25px;
		height: 25px;
		margin: 0 auto;
		position: relative;
		border: 3px solid #222;
	}

	.transportLight:after {
		content: '';
		width: 4px;
		height: 4px;
		border-radius: 50%;
		position: absolute;
		background-color: rgba(255, 255, 255, 0.5);
		top: 6px;
		left: 6px;
		box-shadow: 3px 4px 7px 8px rgba(0, 120, 0, 0.6);
	}

	.transportLightActive {
		background-color: #00AA00;
		box-shadow: 0px 0px 10px 5px rgba(0, 255, 0, 0.4);
		border: 3px solid rgba(0, 120, 0, 1);
	}

	.transportLightActive:after {
		background-color: rgba(255,255,255,1);
		box-shadow: 4px 4px 6px 7px rgba(0, 255, 0, 1);
	}
</style>

