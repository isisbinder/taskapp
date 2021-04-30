<template>
	<span
		class="input-group-text bi task-action action-done fw-bold"
		:class="getActionClasses" 
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
	float: left;
	font-size: 1.5em;
	padding-top: 0;
	padding-bottom: 0;
	padding-left: 0;
}
</style>