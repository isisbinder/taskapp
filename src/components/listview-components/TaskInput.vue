<template>
	<div class="input-group">
		<span class="input-group-text bg-dark text-white border-0">
			<span class="bi" :class="toggleIconClass" style="font-size:2em"/>
		</span>
		<input
			type="text"
			placeholder="Adicionar uma tarefa"
			required
			maxlength="100"
			size="70"
			class="form-control-lg bg-dark text-white border-0 px-2 col-lg-9 col-md-9"
			@focus="changeFocus"
			@blur="changeFocus"
			@keypress.enter="addTask"
		/>
	</div>
</template>

<script>
export default {
	emits: ['add-new-task'],
	data() {
		return {
			isInputFocused: false,
		};
	},
	computed: {
		toggleIconClass() {
			const defaultIconClasses = { "bi-plus": true };
			const focusedIconClasses = { "bi-circle": true };
			return this.isInputFocused ? focusedIconClasses : defaultIconClasses;
		},
	},
	methods: {
		changeFocus() {
			this.isInputFocused = !this.isInputFocused;
		},
		addTask(event) {
			const taskTitle = event.target.value.trim();
			this.emitter.emit('add-new-task', taskTitle);
			event.target.value = '';
		}
	},
};
</script>

<style scoped>
.form-control-lg:focus {
	box-shadow: none;
}
.form-control-lg:focus-visible{
	outline: none;
}
</style>