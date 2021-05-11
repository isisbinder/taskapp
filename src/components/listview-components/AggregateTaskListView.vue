<template>
  <ul class="list-unstyled">
    <template v-for="list in openTasks" :key="list.taskList">
      <task v-for="task in list.tasks" :key="task.id" :task="task" :listName="list.taskList">
        <template v-slot:taskListName><p class="small fst-italic badge bg-danger m-0">@{{ list.taskList }}</p></template>
      </task>
    </template>
  </ul>
</template>

<script>
import Task from './task/Task.vue';

export default {
  inject:['selectedList', 'nonAggLists'],
  components: {
    Task,
  },
  computed: {
    openTasks() {
      let tmpList = [];
      this.nonAggLists.forEach(L => tmpList.push({'taskList': L.name, 'tasks': L.tasks.filter(T => T.isImportant == true)}));
      return tmpList;
    },
	}
}
</script>