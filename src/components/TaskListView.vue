<template>
	<div class="container list-view-container">
		<div class="fixed-list-view pt-3">
			<open-tasks-list></open-tasks-list>
			<done-tasks-list></done-tasks-list>
		</div>
		<task-input class="fixed-input-view my-4"></task-input>
	</div>
</template>

<script>
import DoneTasksList from './list/DoneTasksList.vue';
import OpenTasksList from "./list/OpenTasksList.vue";
import TaskInput from "./TaskInput.vue";

function sorterTaskArray(a, b) {
	if (a['isImportant'] && b['isImportant']) {
		return 0;
	} else if (a['isImportant'] && !b['isImportant']) {
		return -1;
	}
	return 1;
}

export default {
	components: {
		OpenTasksList,
		DoneTasksList,
		TaskInput,
	},
	provide() {
		return {
			allTasks: this.tasks,
			toggleImportantFlag: this.toggleImportantFlag,
			toggleDoneFlag: this.toggleDoneFlag,
			addTask: this.addTask,
		};
	},
	data() {
		return {
			taskRepo: [	],
		};
	},
	computed: {
		tasks() {
			return this.taskRepo;
		}
	},
	methods: {
		addTask(newTask) {
			this.taskRepo.push(newTask);
		},
		toggleImportantFlag(taskTitle) {
			let chosenTask = this.taskRepo.find((t) => t.title === taskTitle);
			let currentStatus = chosenTask.isImportant;
			chosenTask.isImportant = !currentStatus;
			this.taskRepo.sort(sorterTaskArray);
		},
		toggleDoneFlag(taskTitle) {
			let chosenTask = this.taskRepo.find((t) => t.title === taskTitle);
			let currentStatus = chosenTask.isDone;
			chosenTask.isDone = !currentStatus;
		}
	},
};
</script>

<style scoped>
.list-view-container {
	height:100vh;
	width:60%;
}
.fixed-list-view {
	height: 90vh;
}
.fixed-input-view {
	width:100%;
}
</style>