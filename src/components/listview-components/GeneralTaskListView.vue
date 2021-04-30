<template>
  <ul>
    <task v-for="task in openTasks" :key="task.id" :task="task"></task>
  </ul>

  <div class="accordion" v-show="finishedTasksCount > 0">
		<div class="accordion-item border-0 bg-transparent">
			<h2 class="accordion-header">
				<button
					type="button"
					class="accordion-button bg-dark text-white"
					data-bs-toggle="collapse"
					data-bs-target="#doneTasksList"
					aria-expanded="true"
					aria-controls="doneTasksList">
					<span class="done-text">Concluídas</span>
					<span class="badge bg-primary done-count">{{ finishedTasksCount }}</span>
				</button>
			</h2>
			<div id="doneTasksList" class="accordion-collapse collapse pt-3" >
				<ul class="list-group">
					<task
						v-for="task in finishedTasks"
						:key="task.id"
						:task="task"></task>
				</ul>
			</div>
		</div>
	</div>

</template>

<script>
import Task from './task/Task.vue';

export default {
  inject:['selectedList'],
  components: {
    Task,
  },
  computed: {
    finishedTasks() {
      return this.selectedList.value.tasks.filter(T => T.isDone);
    },
    openTasks() {
      return this.selectedList.value.tasks.filter(T => T.isDone == false);
    },
    finishedTasksCount() {
      return this.selectedList.value.tasks.filter(T => T.isDone).length;
    }
	}
}
</script>

<style scoped>
.accordion-button::after {
	color: white;
}
.done-text {
	flex:1;
}
.done-count {
	margin-right: 1em;
}
</style>