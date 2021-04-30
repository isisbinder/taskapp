<template>
  <h1>
    <span class="bi" :class="getListIcon"/>{{ selectedList.value.name }}
  </h1>
  <general-task-list-view></general-task-list-view>
  <task-input class="mt-4 justify-content-center"></task-input>
</template>

<script>
import TaskInput from "./TaskInput.vue";
import GeneralTaskListView from "./GeneralTaskListView.vue";

export default {
  components: {
    TaskInput,
    GeneralTaskListView,
  },
  inject: ['selectedList'],
  computed: {
    getListIcon() {
      return this.selectedList.value.icon;
    }
  }
}
</script>