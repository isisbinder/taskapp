<template>
	<button type="button" class="btn btn-primary" @click.left="this.emitter.emit('show-add-list-input')">
		<span class="bi bi-plus" />Nova lista
	</button>
</template>

<script>
export default {
	emits: ['show-add-list-input'],
}
</script>