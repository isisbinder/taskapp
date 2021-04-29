<template>
	<ul class="lists-group">
		<li
			v-for="list in allLists"
			:key="list.name"
			class="list-group-item border-0"
			:class="getSelectedListClasses(list.name)"
			@click.left="changeSelectedList(list.name)">

			<div class="d-flex justify-content-between align-items-center">
				<span class="bi" :class="list.icon" style="flex: 1"></span>
				<span style="flex: 4">{{ list.name }}</span>
				<span class="badge bg-primary" style="flex: 0.2">{{	getNumberOfTasks(list.name)	}}</span>
			</div>
		</li>
	</ul>
</template>

<script>
export default {
	inject: ["allLists", "importantTasksQty"],
	emits: ['change-list'],
	data() {
		return {
			selectedList: "Tarefas",
		};
	},
	methods: {
		getSelectedListClasses(listName) {
			return {
				active: this.selectedList === listName,
				"bg-transparent": this.selectedList != listName,
			};
		},
		changeSelectedList(listName) {
			this.selectedList = listName;
			this.emitter.emit('change-list', listName);
		},
		getNumberOfTasks(listName) {
			if (listName === "Importante") {
				return this.importantTasksQty();
			}
			const list = this.allLists.find((L) => L.name === listName);
			return list.tasks == undefined ? 0 : list.tasks.length;
		},
	},
};
</script>

<style scoped>
.lists-menu {
	list-style-type: none;
	padding-inline-start: 0;
}
.lists-menu > li {
	line-height: 3em;
	padding-left: 1.2em;
	border-left: 4px solid transparent;
}
.list-group-item {
	cursor: pointer;
}
</style>
