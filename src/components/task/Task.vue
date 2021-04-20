<template>
	<div class="input-group mb-3 rounded-3">
		<li class="list-group-item">
			<task-done-button
				:isDone="task.isDone"
				@click.left="toggleDoneFlag(task.title)"
			/>
			<span :class="getTextClasses">{{ task.title }}</span>
			<task-important-button
				:isImportant="task.isImportant"
				@click.left="toggleImportantFlag(task.title)"
			/>
		</li>
	</div>
</template>

<script>
import TaskDoneButton from "./TaskDoneButton.vue";
import TaskImportantButton from "./TaskImportantButton.vue";
export default {
	components: {
		TaskDoneButton,
		TaskImportantButton,
	},
	props: {
		task: {
			required: true,
			type: Object,
		},
	},
	inject: ["toggleImportantFlag", "toggleDoneFlag"],
	computed: {
		getTextClasses() {
			return this.task.isDone? {'strike-text': true}: {};
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