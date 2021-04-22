<template>
	<div class="input-group">
		<span class="input-group-text bg-dark text-white border-0">
			<span class="bi" :class="getIconClass" style="font-size:2em"/>
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
			@keypress.enter="preAddTask"
		/>
	</div>
</template>

<script>
export default {
	inject: ['addTask'],
	data() {
		return {
			isInputFocused: false,
		};
	},
	computed: {
		getIconClass() {
			const defaultIconClasses = { "bi-plus": true };
			const focusedIconClasses = { "bi-circle": true };
			return this.isInputFocused ? focusedIconClasses : defaultIconClasses;
		},
	},
	methods: {
		changeFocus() {
			this.isInputFocused = !this.isInputFocused;
		},
		preAddTask(event) {
			let newTask = { title: event.target.value, isImportant: false, isDone: false };
			this.addTask(newTask);
      event.target.value = '';
		},
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