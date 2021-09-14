<template>
	<main>
		<div class="container-fluid py-5">
			<div class="row g-5">
				<Showcard v-for="result in results" :key="result.id" :result="result" />
			</div>
		</div>
	</main>
</template>

<script>
import Showcard from "./Showcard.vue";

export default {
	name: "Main",
	props: ["results"],
	components: {
		Showcard,
	},
};
</script>

<style scoped lang="scss">
main {
	background-color: rgb(70, 67, 67);
}
</style>
