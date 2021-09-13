<template>
	<div id="card">
		<ul>
			<li>
				<img :src="`${imgBaseUrl}${result.poster_path}`" alt="" />
			</li>
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
					class="flag-img"
					:src="require(`../assets/images/${result.original_language}.png`)"
					alt=""
				/>
			</li>
			<li v-else>{{ result.original_language }}</li>
			<!-- voto -->
			<li v-html="starCount"></li>
		</ul>
	</div>
</template>

<script>
export default {
	name: "Card",
	props: ["result"],
	data() {
		return {
			imgBaseUrl: "https://image.tmdb.org/t/p/w342",
		};
	},
	computed: {
		starCount() {
			const fiveCount = Math.floor(this.result.vote_average / 2);
			let stars = ``;
			for (let i = 0; i < 5; i++) {
				if (i < fiveCount) {
					stars += '<i class="fas fa-star"></i> ';
				} else {
					stars += '<i class="far fa-star"></i> ';
				}
			}
			return stars;
		},
	},
};
</script>

<style scoped lang="scss">
#card {
	border: 1px solid black;
	margin: 5px;

	.flag-img {
		width: 100px;
	}
}
</style>
