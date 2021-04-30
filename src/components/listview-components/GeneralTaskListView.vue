<template>
  <ul>
    <task v-for="task in selectedList.value.tasks" :key="task.id" :task="task"></task>
  </ul>
</template>

<script>
import Task from './task/Task.vue';

export default {
  inject:['selectedList'],
  components: {
    Task,
  }
}
</script>