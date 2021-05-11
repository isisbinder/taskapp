<template>
	<span
		class="input-group-text bi task-action action-done fw-bold py-0"
		:class="getActionClasses" 
		:title="getActionTitle"
		@mouseover="changeHoverStatus"
		@mouseout="changeHoverStatus"
	/>
</template>

<script>
export default {
	props: {
		isDone: {
			required: true,
			type: Boolean,
		},
	},
	data() {
		return { isHover: false }
	},
	computed: {
		getActionClasses() {
			const defaultDoneIcon = { "bi-circle": true };
			const checkedDoneIcon = { "bi-check-circle-fill": true };
			const hoverDoneIcon = {'bi-check-circle': this.isHover};

			if (this.$props.isDone === false) {
				return this.isHover? hoverDoneIcon : defaultDoneIcon;
			}
			return checkedDoneIcon;
		},
		getActionTitle() {
			return this.$props.isDone? "Desmarcar" : "Marcar como concluída";
		}
	},
	methods: {
		changeHoverStatus() {
			this.isHover = !this.isHover;
		}
	}
};
</script>

<style scoped>
.action-done {
	font-size: 1.5em;
	flex: 0 0 3%
}
</style>