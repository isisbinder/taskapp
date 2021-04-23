<template>
	<ul class="lists-menu">
		<li :class="getSelectedClass('Tarefas')">
			<menu-entry icon="bi-house-door" title="Tarefas"></menu-entry>
		</li>
		<li :class="getSelectedClass('Importante')">
			<menu-entry icon="bi-star" title="Importante"></menu-entry>
		</li>
		<li v-for="list in nonDefaultLists" :key="list.taskListName" :class="getSelectedClass(list.taskListName)">
			<menu-entry :title="list.taskListName"></menu-entry>
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
	inject: ["allLists"],
	data() {
		return {
			showListInput: false,
			selectedList: 'Tarefas',
		}
	},
	computed: {
		nonDefaultLists() {
			return this.allLists.filter((L) => L.taskListName != "Tarefas");
		},
	},
  methods: {
		getSelectedClass(listName) {
			return {'list--selected': this.selectedList === listName}
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
}
.lists-menu > li.list--selected {
	background-color: rgba(55,228,185,0.2);
	color: #00867c;
	font-weight: bold;
	border-left: 4px solid #00867c;
}
</style>