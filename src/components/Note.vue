<template>
	<div class="noteContainer" @click="handleClick">
		<div class="note" v-bind:class="{active : active}"></div>
	</div>
</template>

<script>
export default {
	props: ['active', 'id'],
	methods: {
		handleClick() {
			this.$emit('noteClick', this.id);
		}
	}
}
</script>

<style>
	.noteContainer {
		width: 100px;
		height: 70px;
		background: none;
		float: left;
	}
	.note {
		border-radius: 50%;
		background-color: #220000;
		width: 30px;
		height: 30px;
		position: relative;
		cursor: pointer;
		margin: 20px auto;
		border: 3px solid #222;
	}

	.active {
		background-color: #AA0000;
		box-shadow: 0px 0px 10px 5px rgba(255, 0, 0, 0.4);
		border: 3px solid rgba(120, 0, 0, 1);
	}

	.note:after {
		content: '';
		width: 4px;
		height: 4px;
		border-radius: 50%;
		position: absolute;
		background-color: rgba(255, 255, 255, 0.5);
		top: 7px;
		left: 7px;
		box-shadow: 3px 4px 7px 9px rgba(180, 0, 0, 0.6);
	}

	.active:after {
		background-color: rgba(255,255,255,1);
		box-shadow: 4px 4px 6px 7px rgba(255, 0, 0, 1);
	}
</style>