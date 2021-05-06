<template>
	<span
		class="input-group-text bi task-action action-important py-0"
		:class="getActionClasses"
		title="Marcar como importante"
	></span>
</template>
<script>
export default {
	props: {
		isImportant: {
			required: true,
			type: Boolean,
		},
	},
	computed: {
		getActionClasses() {
			const defaultImportantIcon = { "bi-star": true };
			const checkedImportantIcon = { "bi-star-fill": true };
			return this.$props.isImportant ? checkedImportantIcon : defaultImportantIcon;
		},
	},
};
</script>

<style scoped>
.action-important {
	flex: 0 0 3%
}
</style>