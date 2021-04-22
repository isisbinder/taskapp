<template>
	<div class="container-fluid tasklist-view row p-0 m-0">
		<div class="col px-0 left-side">
			<side-menu></side-menu>
		</div>
		<div class="col pt-3 right-side">
			<div class="tasklist-container col-lg-9 col-md-9">
				<open-tasks-list></open-tasks-list>
				<done-tasks-list></done-tasks-list>
			</div>
			<task-input class="mt-4" style="place-content: center"></task-input>
		</div>
	</div>
</template>

<script>
import SideMenu from './mainmenu/SideMenu.vue';
import DoneTasksList from "./list/DoneTasksList.vue";
import OpenTasksList from "./list/OpenTasksList.vue";
import TaskInput from "./TaskInput.vue";

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
		SideMenu,
		OpenTasksList,
		DoneTasksList,
		TaskInput,
	},
	provide() {
		return {
			allLists: this.tasklists,
			createList: this.createList,
			allTasks: this.tasks,
			toggleImportantFlag: this.toggleImportantFlag,
			toggleDoneFlag: this.toggleDoneFlag,
			addTask: this.addTask,
		};
	},
	data() {
		return {
			taskListsRepo: [{ taskListName: "Tarefas", tasks: [] }],
			taskRepo: [],
		};
	},
	computed: {
		tasks() {
			return this.taskRepo;
		},
		tasklists() {
			return this.taskListsRepo;
		}
	},
	methods: {
		createList(event) {
			console.log('creating new list');
			let name = event.target.value.trim();
			let tasklistTemplate = { taskListName: undefined || name, tasks: [] };
			this.taskListsRepo.push(tasklistTemplate);
			event.target.value = '';
		},
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
		},
	},
};
</script>

<style scoped>
.tasklist-view {
	height: 100vh;
}
.left-side {
	background-color: #f0f8ff;
}

.right-side {
	flex: 4;
}
.tasklist-container {
	height: 87vh;
	margin: auto;
	overflow-y: auto;
}
</style>