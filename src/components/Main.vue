<template>
	<main>
		<Card v-for="result in results" :key="result.id" :result="result" />
	</main>
</template>

<script>
import Card from "./Card.vue";

export default {
	name: "Main",
	props: ["results"],
	components: {
		Card,
	},
};
</script>

<style scoped lang="scss"></style>
