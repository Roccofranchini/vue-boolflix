<template>
	<div>
		<input
			type="text"
			v-model="query"
			:placeholder="placeholder"
			@keyup.enter="emitSearch"
		/>
		<button @click="emitSearch">cerca</button>
	</div>
</template>

<script>
export default {
	name: "Search",
	data() {
		return {
			query: "",
		};
	},
	props: ["placeholder"],
	methods: {
		emitSearch() {
			this.$emit("search", this.query);
		},
	},
};
</script>

<style></style>
