<template>
	<div class="row g-0">
		<main-menu></main-menu>
	</div>
	<div class="row g-0 m-3">
		<new-list-button></new-list-button>
	</div>
</template>

<script>
import MainMenu from "../../main-sidebar-components/Menu.vue";
import NewListButton from "../../main-sidebar-components/NewListButton.vue";

export default {
	components: {
		MainMenu,
    NewListButton,
	},
};
</script>

