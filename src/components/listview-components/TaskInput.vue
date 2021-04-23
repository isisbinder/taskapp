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
			@keypress.enter="addTask"
		/>
	</div>
</template>

<script>
export default {
	inject: ['selectedList'],
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
		addTask(event) {
			let newTaskId = ++this.selectedList.maxId;
			let newTask = { id: newTaskId, title: event.target.value, isImportant: false, isDone: false };		
			this.selectedList.tasks.push(newTask);
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