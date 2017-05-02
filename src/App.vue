<template>
	<div>
		<h1>vue.beats</h1>
		<div class="machine">
			<Controls @togglePlay="togglePlay" @clearPattern="clearPattern"  @changeBpm="changeBpm" :playing="store.playing" :bpm="store.bpm"></Controls>
			<component v-for="stave in store.staves" :key="stave.id" is="stave" :name="stave.name" :notes="stave.notes" @toggleNote="toggleNote"></component>
			<Transporter :pos="store.transporterPos"></Transporter>
		</div>
    	<p class="credits">Built with <a href="https://vuejs.org/" target="_blank">vue.js</a></p>
	</div>
</template>

<script>
	import store from './components/store.js';
	import Controls from './components/Controls.vue';
	import Stave from './components/Stave.vue';
	import Transporter from './components/Transporter.vue';

	export default {
		name: 'app',

		components: { Controls, Stave, Transporter },

		data() { 
			return {
				store: store
			}
		},

		created() {
			this.restorePatterns();
			if (store.playing) {
				this.setTempo();
			}
		},

		methods: {
			setTempo() {
				this.timerId = setInterval(() => this.tick(), this.calculateTempo(store.bpm));
			},
			tick() {
				let transporterPos = store.transporterPos;
				transporterPos++;
				if (transporterPos > 7) {
					transporterPos = 0;
				}
				store.transporterPos = transporterPos;
				this.checkNote();
			},
			calculateTempo(bpm) {
				return 60000 / bpm;
			},
			changeBpm(bpm) {
				store.bpm = bpm;
				if (store.playing) {
					clearInterval(this.timerId);
					this.setTempo();
				}
			},
			toggleNote(note) {
				note.active = !note.active;
				this.savePatterns();
			},
			checkNote() {
				let transporterPos = store.transporterPos;
				let that = this;
				for (var stave of store.staves) {
					for (var note of stave.notes) {
						if (note.active && note.pos === transporterPos) {
							that.playSample(stave.sample);
						}
					}
				}
			},
			playSample(sample) {
				let sound = new Howl({
					src: [sample]
				});
				sound.play();
			},
			togglePlay() {
				if (store.playing) {
					clearInterval(this.timerId);
					store.playing = false;
				} else {
					this.setTempo();
					store.playing = true;
				}
			},
			clearPattern() {
				let staves = store.staves;
				for (var stave of staves) {
					for (var note of stave.notes) {
						note.active = false;
					}
				}
				store.staves = staves;
				this.savePatterns();
			},
			savePatterns() {
				for (var stave of store.staves) {
					localStorage.setItem('vb-pattern-' + stave.id, JSON.stringify(stave.notes));
				}				
			},
			restorePatterns() {
				for (var stave of store.staves) {
					let localStorageRef = localStorage.getItem('vb-pattern-' + stave.id);
					if (localStorageRef) {
						stave.notes = JSON.parse(localStorageRef);
					}
				}
			}
		}
	}
</script>

<style>
	html {
		height: 100%;
	}

	body {
		height: 100%;   
		background: rgba(247,247,247,1);
		background: -moz-radial-gradient(center, ellipse cover, rgba(247,247,247,1) 0%, rgba(246,246,246,1) 47%, rgba(180,180,180,1) 100%);
		background: -webkit-gradient(radial, center center, 0px, center center, 100%, color-stop(0%, rgba(247,247,247,1)), color-stop(47%, rgba(246,246,246,1)), color-stop(100%, rgba(180,180,180,1)));
		background: -webkit-radial-gradient(center, ellipse cover, rgba(247,247,247,1) 0%, rgba(246,246,246,1) 47%, rgba(180,180,180,1) 100%);
		background: -o-radial-gradient(center, ellipse cover, rgba(247,247,247,1) 0%, rgba(246,246,246,1) 47%, rgba(180,180,180,1) 100%);
		background: -ms-radial-gradient(center, ellipse cover, rgba(247,247,247,1) 0%, rgba(246,246,246,1) 47%, rgba(180,180,180,1) 100%);
		background: radial-gradient(ellipse at center, rgba(247,247,247,1) 0%, rgba(246,246,246,1) 47%, rgba(180,180,180,1) 100%);
		filter: progid:DXImageTransform.Microsoft.gradient( startColorstr='#ffffff', endColorstr='#ededed', GradientType=1 );
		font-family: 'Roboto Slab', serif;
	}

	h1 {
		text-shadow: 0 2px 1px rgba(240, 240, 240, 1);
		text-align: center;
	}
	.machine {
		margin: 40px auto;
		width: 910px;
		position: relative;
	}
	.credits {
		width: 99%;
		text-align: center;
		position: absolute;
		bottom: 10px;
	}

	.credits a {
		color: black;
	}
</style>
