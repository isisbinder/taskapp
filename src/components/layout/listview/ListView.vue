<template>
	<div class="tasklist-container col-lg-9 col-md-9">
		<open-tasks-list :tasks="getTasksByDoneStatus(false)"></open-tasks-list>
		<done-tasks-list :tasks="getTasksByDoneStatus(true)"></done-tasks-list>
	</div>
	<task-input class="mt-4" style="place-content: center"></task-input>
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
</style>