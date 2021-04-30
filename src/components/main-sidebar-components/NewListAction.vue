<template>
	<input
		type="text"
		placeholder="Lista sem título"
		class="form-control mt-3"
		v-show="showListInput" 
		@keypress.enter="signalCreateList"/>

	<button
		type="button"
		class="btn btn-primary mt-2"
		@click.left="toggleNewListInput">
		<span class="bi bi-plus"/>Nova lista
	</button>
</template>

<script>
export default {
	emits: ['create-list'],
	data() {
		return {
			showListInput: false,
		};
	},
	methods: {
		toggleNewListInput() {
			this.showListInput = !this.showListInput;
		},
		signalCreateList(event) {
      let name = event.target.value.trim();
      this.emitter.emit('create-list', name);
      event.target.value = "";
      this.showListInput = false;
    },
	},
};
</script>