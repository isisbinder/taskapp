<template>
	<div class="accordion" v-show="hasFinishedTasks">
		<div class="accordion-item border-0 bg-transparent">
			<h2 class="accordion-header">
				<button
					type="button"
					class="accordion-button bg-dark text-white"
					data-bs-toggle="collapse"
					data-bs-target="#doneTasksList"
					aria-expanded="true"
					aria-controls="doneTasksList">
					<span class="done-text">Concluídas</span>
					<span class="badge bg-primary done-count">{{ finishedTasksCount }}</span>
				</button>
			</h2>
			<div id="doneTasksList" class="accordion-collapse collapse pt-3" >
				<ul class="list-group">
					<task
						v-for="currentTask in tasks"
						:key="currentTask.id"
						:task="currentTask"></task>
				</ul>
			</div>
		</div>
	</div>
</template>

<script>
import Task from './task/Task.vue';
export default {
	components: {
		Task,
	},
	inject: ['selectedList'],
	props: {
		tasks: {
			required: true,
		}
	},
	computed: {
		finishedTasksCount() {
			return this.tasks.length;
		},
		hasFinishedTasks() {
			return this.tasks.length > 0;
		}
	}
};
</script>

<style scoped>
.accordion-button::after {
	color: white;
}
.done-text {
	flex:1;
}
.done-count {
	margin-right: 1em;
}
</style>