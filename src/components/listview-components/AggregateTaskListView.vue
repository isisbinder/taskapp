<template>
	<ul class="list-unstyled">
		<template v-for="list in openTasks" :key="list.taskList">
			<task
				v-for="task in list.tasks"
				:key="task.id"
				:task="task"
				:listName="list.taskList"	>
				<template v-slot:taskListName>
          <p class="small fst-italic badge bg-danger m-0">
						@{{ list.taskList }}
					</p>
        </template>
			</task>
		</template>
	</ul>
	<div class="accordion" v-show="finishedTasksCount > 0">
		<div class="accordion-item border-0 bg-transparent">
			<h2 class="accordion-header">
				<button
					type="button"
					class="accordion-button text-white"
					data-bs-toggle="collapse"
					data-bs-target="#doneTasksList"
					aria-expanded="true"
					aria-controls="doneTasksList">
					<span class="done-text">Concluídas</span>
					<span class="badge bg-primary done-count">{{ finishedTasksCount	}}</span>
				</button>
			</h2>
			<div id="doneTasksList" class="accordion-collapse collapse pt-3">
				<ul class="list-group">
					<template v-for="list in finishedTasks" :key="list.taskList">
						<task
							v-for="task in list.tasks"
							:key="task.id"
							:task="task"
							:listName="list.taskList">
							<template v-slot:taskListName>
                <p class="small fst-italic badge bg-danger m-0">
									@{{ list.taskList }}
								</p>
              </template>
						</task>
					</template>
				</ul>
			</div>
		</div>
	</div>
</template>

<script>
import Task from "./task/Task.vue";

export default {
	inject: ["selectedList", "nonAggLists"],
	components: {
		Task,
	},
	computed: {
		openTasks() {
      const tmpList = [];
      for (let list of this.nonAggLists) {
        var tmpTasks = list.tasks.filter(T => this.selectedList.value.taskAggFn(T) && T.isDone == false);
        if (tmpTasks.length > 0) {
          tmpList.push({taskList: list.name, tasks: tmpTasks});
        }
      }
			return tmpList;
		},
		finishedTasks() {
      const tmpList = [];
      for (let list of this.nonAggLists) {
        var tmpTasks = list.tasks.filter(T => this.selectedList.value.taskAggFn(T) && T.isDone == true);
        if (tmpTasks.length > 0) {
          tmpList.push({taskList: list.name, tasks: tmpTasks});
        }
      }
      return tmpList;
		},
    finishedTasksCount() {
      return this.finishedTasks.length;
    }
	},
};
</script>

<style scoped>
.accordion-button {
	background-color: rgba(0,0,0,0.6);
}
.done-text {
	flex:1;
}
.done-count {
	margin-right: 1em;
}
</style>