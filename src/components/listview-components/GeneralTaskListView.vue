<template>
  <ul>
    <li v-for="task in selectedList.value.tasks" :key="task.id">
      {{ task.title }}
    </li>
  </ul>
</template>

<script>
export default {
  inject:['selectedList'],
}
</script>