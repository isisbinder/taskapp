<template>
	<div class="input-group mb-3 rounded-3">
		<li class="list-group-item py-3">
			<div class="container-fluid m-0 p-0">
				<div class="row">
					<task-done-action
						class="col"
						:isDone="task.isDone"
						@click.left="toggleDoneFlag(task.id)"
					/>
					<div class="col m-0 p-0">
						<p :class="getTextClasses" class="m-0">{{ task.title }}</p>
						<slot name="taskListName"></slot>
					</div>
					<task-important-action
						class="col"
						:isImportant="task.isImportant"
						@click.left="toggleImportantFlag(task.id)"
					/>
				</div>
			</div>
		</li>
	</div>
</template>

<script>
import TaskDoneAction from "./TaskDoneAction.vue";
import TaskImportantAction from "./TaskImportantAction.vue";

export default {
	components: {
		TaskDoneAction,
		TaskImportantAction,
	},
	props: {
		task: {
			required: true,
			type: Object,
		},
	},
	inject: ["selectedList"],
	computed: {
		getTextClasses() {
			return { "strike-text": this.task.isDone };
		},
	},
	methods: {
		toggleImportantFlag(taskId) {
			let chosenTask = this.selectedList.value.tasks.find(
				(t) => t.id === taskId
			);
			let currentStatus = chosenTask.isImportant;
			chosenTask.isImportant = !currentStatus;
			this.emitter.emit("sort-selected-list");
		},
		toggleDoneFlag(taskId) {
			let chosenTask = this.selectedList.value.tasks.find(
				(t) => t.id === taskId
			);
			let currentStatus = chosenTask.isDone;
			chosenTask.isDone = !currentStatus;
		},
	},
};
</script>

<style scoped>
.input-group-text {
	border: 1px solid rgba(0, 0, 0, 0.125);
}
.list-group-item {
	width: inherit;
	/*padding: 1em;*/
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