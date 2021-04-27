<template>
	<div class="container-fluid tasklist-view row p-0 m-0">
		<div class="col px-0 left-side">
			<main-side-bar></main-side-bar>
		</div>
		<div class="col pt-3 right-side">
			<list-view></list-view>
		</div>
	</div>
</template>

<script>
import MainSideBar from "./mainmenu/MainSideBar.vue";
import ListView from "./listview/ListView.vue";

export default {
	components: {
		MainSideBar,
		ListView,
	},
	provide() {
		return {
			allLists: this.getAllLists,
			selectedList: this.getSelectedList,
		};
	},
	data() {
		return {
			taskListsRepo: [
				{ taskListName: "Tarefas", icon: "bi-house-door", maxId: 0, tasks: [] },
			],
			selectedListName: "Tarefas",
		};
	},
	computed: {
		getAllLists() {
			return this.taskListsRepo;
		},
		getSelectedList() {
			return this.taskListsRepo.find(
				(o) => o.taskListName === this.selectedListName
			);
		},
	},
	methods: {
		createList(event) {
			let name = event.target.value.trim();
			let tasklistTemplate = { taskListName: "" || name, tasks: [] };
			this.taskListsRepo.push(tasklistTemplate);
			event.target.value = "";
		},
	},
};
</script>

<style scoped>
.tasklist-view {
	height: 100vh;
}
.left-side {
	flex: 0.8;
	background-color: #fdfcfc;
}

.right-side {
	flex: 4;
	background-color: rgba(162,220,211,0.76)
}
.tasklist-container {
	height: 87vh;
	margin: auto;
	overflow-y: auto;
}
</style>