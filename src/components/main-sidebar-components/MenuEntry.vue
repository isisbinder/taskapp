<template>
  <div class="d-flex justify-content-between align-items-center">
  <span class="bi entry-icon" :class="icon" style="flex:1"></span>
  <span style="flex:4">{{ title }}</span>
  <span class="badge bg-primary" style="flex:0.2">{{ tasksQty }}</span>
  </div>
</template>

<script>
export default {
  props: {
    title: {
      required: false,
      type: String,
      default: 'Lista sem título',
    },
    icon: {
      required: false,
      type: String,
      default: 'bi-list'
    },
    tasksQty: {
      required: true,
      type: Number
    }
  },
}
</script>

<style scoped>
.lists-menu .entry-icon::before {
	margin-right: 2em;
}
</style>