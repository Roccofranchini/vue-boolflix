<template>
	<div id="card">
		<ul>
			<!-- titolo -->
			<li v-if="!result.title">{{ result.name }}</li>
			<li v-else>{{ result.title }}</li>
			<!-- titolo originale -->
			<li v-if="!result.title">{{ result.original_name }}</li>
			<li v-else>{{ result.original_title }}</li>
			<!-- lingua originale -->
			<li v-if="result.original_language == ('en' || 'it')">
				<img :src="`../assets/images/${result.original_language}.png`" alt="" />
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
}
</style>
