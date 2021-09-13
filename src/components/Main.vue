<template>
	<main>
		<div class="container-fluid py-5">
			<div class="row g-5">
				<Card v-for="result in results" :key="result.id" :result="result" />
			</div>
		</div>
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

<style scoped lang="scss">
main {
	background-color: rgb(70, 67, 67);
}
</style>
