<template>
	<div class="container-fluid tasklist-view row p-0 m-0">
		<div class="col px-0 left-side">
			<div class="row g-0">
				<task-list-listing></task-list-listing>
			</div>
			<div class="row g-0 m-3">
				<new-list-action></new-list-action>
			</div>
		</div>
		<div class="col py-4 px-5 right-side">
			<list-view></list-view>
		</div>
	</div>
</template>

<script>
import { computed } from 'vue';
import TaskListListing from "./components/main-sidebar-components/TaskListListing.vue";
import NewListAction from "./components/main-sidebar-components/NewListAction.vue";
import ListView from "./components/listview-components/ListView.vue";

function sorterTaskArray(a, b) {
	if (a["isImportant"] && b["isImportant"]) {
		return 0;
	} else if (a["isImportant"] && !b["isImportant"]) {
		return -1;
	}
	return 1;
}

export default {
	name: "App",
	components: {
		TaskListListing,
		NewListAction,
		ListView,
	},
	provide() {
		return {
			nonAggLists: this.taskLists,
			aggLists: this.aggregateLists,
			selectedList: computed(() => this.findListByName(this.selectedList)),
			selectedListName: computed(() => this.selectedList),
		};
	},
	data() {
		return {
			taskLists: [
				{
					name: "Tarefas",
					icon: "bi-house-door",
					maxTaskId: 0,
					tasks: [],
				}
			],
			aggregateLists: [
				{ name: 'Importante', icon: 'bi-exclamation-octagon', taskAggFn: (T) => T.isImportant == true}
			],
			selectedList: "Tarefas",
			defaultListName: "Lista sem nome",
		};
	},
	methods: {
    getListMaxTaskId(listName) {
      return this.taskLists.find(L => L.name === listName).maxTaskId;
    },
		buildDefaultListName() {
			const regex = new RegExp("^" + this.defaultListName, "i");

			const listasSemNome = this.taskLists.filter((L) => L.name.match(regex));

			const qtdeListasSemNome =
				Math.max(0, ...listasSemNome.flatMap((N) => N.name.match(/\d+/))) + 1;

			return this.defaultListName + ' ' + qtdeListasSemNome;
		},
		findListByName(listName) {
			return Array.of(...this.taskLists, ...this.aggregateLists).find(L => L.name === listName);
		},
	},
	mounted() {
    this.emitter.on('change-list', (listName) => {
      this.selectedList = listName;
    }),
		this.emitter.on("create-list", (listName) => {
			const newListName = listName || this.buildDefaultListName();

			const tasklistTemplate = {
				name: newListName,
				icon: "bi-list",
				maxTaskId: 0,
				tasks: [],
			};

			this.taskLists.push(tasklistTemplate);
		}),
    this.emitter.on("add-new-task", (taskTitle) => {
			let targetList = this.findListByName(this.selectedList);
			const taskId = targetList.maxTaskId + 1;
			const newTask = {id: taskId, title: taskTitle, isDone: false, isImportant: false};
			targetList.tasks.push(newTask);
			targetList.maxTaskId = taskId;
    }),
		this.emitter.on("sort-list", (listName) => {
			this.taskLists.find(L => L.name === listName).tasks.sort(sorterTaskArray);
		}),
		this.emitter.on("toggle-important-at-list", (targetObject) => {
			const targetList = this.findListByName(targetObject.listName);
			const task = targetList.tasks.find(T => T.id === targetObject.id);
			task.isImportant = !task.isImportant;
			this.emitter.emit("sort-list", targetList.name);
		})
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
	background-color: rgba(162, 220, 211, 0.76);
}
.tasklist-container {
	height: 87vh;
	margin: auto;
	overflow-y: auto;
}
</style>
