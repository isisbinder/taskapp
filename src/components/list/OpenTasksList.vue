<template>
	<ul class="list-group">
		<task
			v-for="currentTask in this.openTasks"
			:key="currentTask.title"
			:task="currentTask"
			title="Marcar como concluído"
		></task>
	</ul>
</template>

<script>
import Task from "../task/Task.vue";
export default {
	components: {
		Task,
	},
	inject: ['allTasks'],
	computed: {
		openTasks() {
			return this.allTasks.filter(f => f.isDone === false);
		}
	}
};
</script>