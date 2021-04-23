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
import MainSideBar from './mainmenu/MainSideBar.vue';
import ListView from './listview/ListView.vue';

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
				{ taskListName: "Tarefas", 
					maxId: 0, 
					tasks: []
				}
			],
			selectedListName: 'Tarefas',
		};
	},
	computed: {
		getAllLists() {
			return this.taskListsRepo;
		},
		getSelectedList() {
			return this.taskListsRepo.find((o) => o.taskListName === this.selectedListName);
		}
	},
	methods: {
		createList(event) {
			let name = event.target.value.trim();
			let tasklistTemplate = { taskListName: '' || name, tasks: [] };
			this.taskListsRepo.push(tasklistTemplate);
			event.target.value = '';
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