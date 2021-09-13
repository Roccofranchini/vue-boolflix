<template>
	<div id="Search">
		<div class="input-group">
			<input
				type="text"
				class="form-control"
				v-model="query"
				@keyup.enter="emitSearch"
				:placeholder="placeholder"
				aria-label="Recipient's username"
				aria-describedby="button-addon2"
			/>
			<button
				class="btn btn-danger x-3"
				type="button"
				id="button-addon2"
				@click="emitSearch"
			>
				Cerca
			</button>
		</div>
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

<style scoped lang="scss"></style>
