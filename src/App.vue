<template>
	<task-list-view></task-list-view>
</template>

<script>
import TaskListView from "./components/TaskListView.vue";

export default {
	name: "App",
	components: {
		TaskListView,
	},
};
</script>

<style>
/*#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}*/
</style>
