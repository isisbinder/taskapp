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
		<div class="col pt-3 right-side">
      <task-input class="mt-4 justify-content-center"></task-input>
		</div>
	</div>
</template>

<script>
import TaskListListing from "./components/main-sidebar-components/TaskListListing.vue";
import NewListAction from "./components/main-sidebar-components/NewListAction.vue";
import TaskInput from "./components/listview-components/TaskInput.vue";

export default {
	name: "App",
	components: {
		TaskListListing,
		NewListAction,
    TaskInput,
	},
	provide() {
		return {
			allLists: this.taskLists,
			chosenList: this.selectedList,
      importantTasksQty: this.getImportantTasksQty,
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
				},
				{
					name: "Importante",
					icon: "bi-exclamation-octagon",
					maxTaskId: undefined,
					tasks: undefined,
				},
			],
			selectedList: "Tarefas",
			defaultListName: "Lista sem nome",
		};
	},
	methods: {
    getTaskListIcon() {
      return this.taskLists.find(L => L.name === this.selectedList).icon;
    },
    getListMaxTaskId(listName) {
      return this.taskLists.find(L => L.name === listName).maxTaskId;
    },
    getImportantTasksQty() {
      const allImportantTasks = this.taskLists.filter(L => L.name != 'Importante').flatMap(o => o.tasks).filter(t => t.isImportant == true);
      return allImportantTasks.length;
    }
	},
	mounted() {
    this.emitter.on('change-list', (listName) => {
      this.selectedList = listName;
    }),
		this.emitter.on("create-list", (listName) => {
			const regex = new RegExp("^" + this.defaultListName, "i");

			const listasSemNome = this.taskLists.filter((L) => L.name.match(regex));

			const qtdeListasSemNome =
				Math.max(0, ...listasSemNome.flatMap((N) => N.name.match(/\d+/))) + 1;

			const tasklistTemplate = {
				name: listName + " " + qtdeListasSemNome,
				icon: "bi-list",
				maxTaskId: 0,
				tasks: [],
			};

			this.taskLists.push(tasklistTemplate);
		}),
    this.emitter.on("add-new-task", (taskTitle) => {
      // Quando a lista selecionada for 'Importante', adicionar na tarefas, mas marcar como importante
			const listName = this.selectedList === 'Importante'? 'Tarefas' : this.selectedList;
      const targetList = this.taskLists.find(L => L.name === listName);

      const taskId = this.getListMaxTaskId(listName) + 1;
      const isImportantTask = this.selectedList === 'Importante';
      const taskObject = {id: taskId, title: taskTitle, isDone: false, isImportant: isImportantTask};
      targetList.tasks.push(taskObject);
      targetList.maxTaskId = taskId;
    });
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
.tasklist-container h1 {
	color: #005d67;
}
.tasklist-container h1 > span.bi {
	margin-right: 0.3em
}
</style>
