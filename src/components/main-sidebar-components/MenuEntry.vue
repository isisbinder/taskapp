<template>
  <span class="bi entry-icon" :class="icon">
    {{ title }} [contagem]
  </span>
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
    }
  },
}
</script>

<style scoped>
.lists-menu .entry-icon::before {
	margin-right: 2em;
}
</style>