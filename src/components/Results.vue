<template>
	<section class="py-5">
		<div class="container-fluid py-5">
			<h2 class="pb-5 ps-4">{{ title }}</h2>
			<div class="row g-5">
				<Card v-for="item in items" :key="item.id" :item="item" />
			</div>
		</div>
	</section>
</template>

<script>
import Card from "./Card.vue";

export default {
	name: "Result",
	props: ["items", "title"],
	components: {
		Card,
	},
};
</script>

<style scoped lang="scss">
section {
	background-color: rgb(70, 67, 67);
	h2 {
		color: white;
		text-align: left;
	}
}
</style>
