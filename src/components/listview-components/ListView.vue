<template>
  <h1>
    <span class="bi" :class="getListIcon"/>{{ selectedList.value.name }}
  </h1>
  <task-input class="mt-4 justify-content-center"></task-input>
</template>

<script>
import TaskInput from "./TaskInput.vue";

export default {
  components: {
    TaskInput,
  },
  inject: ['selectedList'],
  computed: {
    getListIcon() {
      return this.selectedList.value.icon;
    }
  }
}
</script>