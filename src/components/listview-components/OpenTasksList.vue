<template>
	<ul class="list-group">
		<task
			v-for="currentTask in tasks"
			:key="currentTask.id"
			:task="currentTask"
		></task>
	</ul>
</template>

<script>
import Task from "./task/Task.vue";
export default {
	components: {
		Task,
	},
	props: {
		tasks: {
			required: true,
		}
	}
};
</script>