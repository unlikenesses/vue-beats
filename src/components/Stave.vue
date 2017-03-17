<template>
	<div class="stave">
		<div class="staveName">{{ name }}</div>
		<component v-for="note in notes" :id="note.id" :key="note.id" is="note" :active="note.active" @noteClick="note.active = !note.active"></component>
	</div>
</template>

<script>
	import Note from './Note.vue';

	export default {
		props: ['name', 'notes'],
		components: { Note }
	}
</script>

<style>
	.stave {
		width: 100%;
		height: 70px;
		border: 1px solid #666;
		background: #333;
	}

	.staveName {
		float: right;
		color: white;
		margin: 20px 10px 0 0;
		background: #111;
		width: 80px;
		padding: 3px 8px 3px 8px;
	}
</style>