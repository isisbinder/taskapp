<template>
	<div class="input-group mb-3 rounded-3">
		<li class="list-group-item">
			<task-done-action 
				:isDone="task.isDone"
				@click.left="toggleDoneFlag(task.id)"/>
			<span :class="getTextClasses">{{ task.title }}</span>
			<task-important-button
				:isImportant="task.isImportant"
				@click.left="toggleImportantFlag(task.id)"/>
		</li>
	</div>
</template>

<script>
import TaskDoneAction from "./TaskDoneAction.vue";
import TaskImportantButton from "./TaskImportantButton.vue";

function sorterTaskArray(a, b) {
	if (a["isImportant"] && b["isImportant"]) {
		return 0;
	} else if (a["isImportant"] && !b["isImportant"]) {
		return -1;
	}
	return 1;
}

export default {
	components: {
		TaskDoneAction,
		TaskImportantButton,
	},
	props: {
		task: {
			required: true,
			type: Object,
		},
	},
	inject: ['selectedList'],
	computed: {
		getTextClasses() {
			return this.task.isDone? {'strike-text': true}: {};
		}
	}, 
	methods: {
		toggleImportantFlag(taskId) {
			let chosenTask = this.selectedList.tasks.find((t) => t.id === taskId);
			let currentStatus = chosenTask.isImportant;
			chosenTask.isImportant = !currentStatus;
			this.selectedList.tasks.sort(sorterTaskArray);
		},
		toggleDoneFlag(taskId) {
			let chosenTask = this.selectedList.tasks.find((t) => t.id === taskId);
			let currentStatus = chosenTask.isDone;
			chosenTask.isDone = !currentStatus;
		}
	}
};
</script>

<style scoped>
.input-group-text {
	border: 1px solid rgba(0, 0, 0, 0.125);
}
.list-group-item {
	width: inherit;
	padding: 1em;
}
.list-group-item:hover {
	background-color: rgb(240, 240, 240);
}
.task-action {
	background-color: transparent;
	border: 0 none;
	color: rgba(0, 0, 0, 0.6);
}
.task-action:hover {
	cursor: pointer;
}
.strike-text {
	text-decoration: line-through;
}
</style>