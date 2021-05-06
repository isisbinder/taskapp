<template>
	<input
		type="text"
		placeholder="Lista sem título"
		class="form-control mt-3"
		v-show="showListInput"
		@keypress.enter="signalCreateList"
		@keyup.esc="toggleNewListInput"
		ref="newListInput"
	/>
	<p v-show="showListInput" class="text-muted small fst-italic">
		Para ocultar o campo pressione <kbd>ESC</kbd>
	</p>
	<button
		type="button"
		class="btn btn-primary mt-2"
		@click.left="toggleNewListInput"
	>
		<span class="bi bi-plus" />Nova lista
	</button>
</template>

<script>
export default {
	emits: ["create-list"],
	data() {
		return {
			showListInput: false,
		};
	},
	methods: {
		toggleNewListInput() {
			this.showListInput = !this.showListInput;
			this.$nextTick(() => {
				if (this.showListInput) {
					this.focusInput();
				}
			});
		},
		focusInput() {
			this.$refs.newListInput.focus();
		},
		signalCreateList(event) {
			let name = event.target.value.trim();
			this.emitter.emit("create-list", name);
			event.target.value = "";
			this.showListInput = false;
		},
	},
};
</script>
