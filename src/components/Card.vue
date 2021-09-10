<template>
	<div id="card">
		<ul v-if="!result.title">
			<li>{{ result.name }}</li>
			<li>{{ result.original_language }}</li>
		</ul>
		<ul v-else>
			<li>{{ result.title }}</li>
			<li>{{ result.original_language }}</li>
		</ul>
	</div>
</template>

<script>
export default {
	name: "Card",
	props: ["result"],
};
</script>

<style scoped lang="scss">
#card {
	border: 1px solid black;
	margin: 5px;
}
</style>
