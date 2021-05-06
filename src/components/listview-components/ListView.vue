<template>
  <h1 class="mb-4">
    <span class="bi" :class="getListIcon"/>{{ selectedList.value.name }}
  </h1>
  <component :is="currentListViewType"></component>
  <task-input class="mt-4 justify-content-center" v-show="!isAggList"></task-input>
</template>

<script>
import TaskInput from "./TaskInput.vue";
import GeneralTaskListView from "./GeneralTaskListView.vue";
import AggregateTaskListView from "./AggregateTaskListView.vue";

export default {
  components: {
    TaskInput,
    GeneralTaskListView,
    AggregateTaskListView,
  },
  inject: ['selectedList'],
  computed: {
    getListIcon() {
      return this.selectedList.value.icon;
    },
    currentListViewType() {
      return this.isAggList? 'AggregateTaskListView' : 'GeneralTaskListView';
    },
    isAggList() {
      return Object.prototype.hasOwnProperty.call(this.selectedList.value, 'taskAggFn');
    }
  }
}
</script>

<style scoped>
h1 {
	color: #005d67;
}
span.bi {
	margin-right: 0.3em
}
</style>