<template>
	<ul class="list-group list-unstyled">
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
	inject: ['selectedListName', 'aggLists', 'nonAggLists'],
	emits: ['change-list'],
	computed: {
		allLists() {
			return Array.of(...this.aggLists, ...this.nonAggLists);
		}
	},
	methods: {
		getSelectedListClasses(listName) {
			return {
				active: this.selectedListName.value === listName,
				"bg-transparent": this.selectedListName.value != listName,
			};
		},
		changeSelectedList(listName) {
			this.emitter.emit('change-list', listName);
		},
		getNumberOfTasks(listName) {
			const aggList = this.aggLists.find(L => L.name === listName);
			if (aggList) {
				const allAggTasks = this.nonAggLists.flatMap(o => o.tasks).filter(aggList.taskAggFn);
				return allAggTasks == undefined? 0: allAggTasks.length;
			}
			const list = this.nonAggLists.find(L => L.name === listName);
			return list.tasks == undefined? 0 : list.tasks.length;
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
	border-radius: 0
}
</style>
