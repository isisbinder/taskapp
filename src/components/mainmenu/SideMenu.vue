<template>
  <div class="row g-0">
    <ul class="lists-menu">
      <li>
        <task-list-entry icon="bi-house-door" title="Tarefas"></task-list-entry>
      </li>
      <li>
        <task-list-entry icon="bi-star" title="Importante"></task-list-entry>
      </li>
      <li v-for="list in nonDefaultLists" :key="list.taskListName">
        <task-list-entry :title="list.taskListName"></task-list-entry>
      </li>
      <li>
        <input
          type="text"
          placeholder="Lista sem título"
          class="form-control mt-3"
          style="width:80%"
          @keypress.enter="createList"
        />
      </li>
    </ul>
  </div>

  <div class="row g-0 m-3">
    <button
      type="button"
      class="btn btn-primary">
      <span class="bi bi-plus" />Nova lista
    </button>
  </div>
</template>

<script>
import TaskListEntry from "./SideMenuEntry.vue";
export default {
  components: {
    TaskListEntry,
  },
  inject: ["allLists", "createList"],
 
  computed: {
    nonDefaultLists() {
      return this.allLists.filter((L) => L.taskListName != "Tarefas");
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
}
</style>
