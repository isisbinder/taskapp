<template>
	<div class="tasklist-container col-lg-9 col-md-9">
		<h1 class="mb-4"><span class="bi" :class="getTaskListIcon"></span>{{ getTaskListName }}</h1>
		<open-tasks-list :tasks="getTasksByDoneStatus(false)"></open-tasks-list>
		<done-tasks-list :tasks="getTasksByDoneStatus(true)"></done-tasks-list>
	</div>
	<task-input class="mt-4 justify-content-center"></task-input>
</template>

<script>
import DoneTasksList from "../../listview-components/DoneTasksList.vue";
import OpenTasksList from "../../listview-components/OpenTasksList.vue";
import TaskInput from "../../listview-components/TaskInput.vue";

export default {
	components: {
		OpenTasksList,
		DoneTasksList,
		TaskInput,
	},
	inject: ["selectedList"],
	computed: {
		getTaskListName() {
			return this.selectedList.taskListName;
		},
		getTaskListIcon() {
			return this.selectedList.icon;
		}
	},
	methods: {
		getTasksByDoneStatus(doneStatus) {
			return this.selectedList.tasks.filter((o) => o.isDone === doneStatus);
		},
	},
};
</script>

<style scoped>
.tasklist-container {
	height: 87vh;
	margin: auto;
	overflow-y: auto;
}
h1 {
	color: #005d67;
}
h1 > span.bi {
	margin-right: 0.3em
}
</style>