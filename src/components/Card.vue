<template>
	<div id="card">
		<ul>
			<!-- titolo -->
			<li>{{ result.name || result.title }}</li>
			<!-- titolo originale -->
			<li>{{ result.original_name || result.original_title }}</li>

			<!-- lingua originale -->
			<li
				v-if="
					result.original_language == 'en' || result.original_language == 'it'
				"
			>
				<img
					:src="require(`../assets/images/${result.original_language}.png`)"
					alt=""
				/>
			</li>
			<li v-else>{{ result.original_language }}</li>
			<!-- voto -->
			<li>{{ result.vote_average }}</li>
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

	img {
		width: 100px;
	}
}
</style>
