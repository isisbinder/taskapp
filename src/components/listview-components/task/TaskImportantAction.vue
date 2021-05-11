<template>
	<span
		class="input-group-text bi task-action action-important py-0"
		:class="getActionClasses"
		:title="getActionTitle"
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
			return this.$props.isImportant? checkedImportantIcon : defaultImportantIcon;
		},
		getActionTitle() {
			return this.$props.isImportant? "Desmarcar" : "Marcar como importante";
		}
	},
};
</script>

<style scoped>
.action-important {
	flex: 0 0 3%
}
</style>