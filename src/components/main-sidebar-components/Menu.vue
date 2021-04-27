<template>
	<ul class="lists-group">
		<li v-for="list in allLists" :key="list.taskListName" class="list-group-item border-0" :class="getSelectedClasses(list.taskListName)">
			<menu-entry :icon="list.icon" :title="list.taskListName" :tasksQty="getNumberOfTasks(list.tasks)"></menu-entry>
		</li>
		<li>
			<input
				type="text"
				placeholder="Lista sem título"
				class="form-control mt-3"
				style="width: 80%"
				@keypress.enter="createList"
				v-show="showListInput"
			/>
		</li>
	</ul>
</template>

<script>
import MenuEntry from './MenuEntry.vue';

export default {
	components: {
		MenuEntry,
	},
	inject: ["allLists", "selectedList"],
	data() {
		return {
			showListInput: false,
		}
	},
  methods: {
		getSelectedClasses(listName) {
			return {'active': this.selectedList.taskListName == listName, 
			'bg-transparent': this.selectedList.taskListName != listName
			}
		},
		getNumberOfTasks(tasksInList) {
			return tasksInList == undefined? 0 : tasksInList.length;
		},		
		createList(event) {
			let name = event.target.value.trim();
			let tasklistTemplate = { taskListName: undefined || name, tasks: [] };
			this.allLists.push(tasklistTemplate);
			event.target.value = "";
			this.showListInput = false;
		},
	},
	mounted() {
    this.emitter.on('show-add-list-input', () => {
      this.showListInput = true;
    });
  }
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
</style>