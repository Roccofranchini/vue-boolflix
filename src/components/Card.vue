<template>
	<div id="card">
		<ul>
			<li v-if="result.poster_path">
				<img :src="`${imgBaseUrl}${result.poster_path}`" alt="" />
			</li>
			<li v-else>
				<img src="../assets/images/images.png" alt="" class="w-342" />
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
			<div v-if="result.vote_average !== 0">
				<span v-for="(n, index) in 5" :key="`${n}-${index}`">
					<i v-if="starCount < index + 1" class="far fa-star"></i
					><i v-else class="fas fa-star"></i>
				</span>
			</div>
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
			const fiveCount = Math.ceil(this.result.vote_average / 2);
			return fiveCount;
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
	.w-342 {
		width: 342px;
	}
}
</style>
