<template>
	<div id="card" class="col col-md-6 col-xl-4">
		<ul class="h-100">
			<div class="hover-card h-100">
				<li v-if="result.poster_path">
					<img
						:src="`${imgBaseUrl}${result.poster_path}`"
						alt=""
						class="copertina"
					/>
				</li>
				<li v-else>
					<img src="../assets/images/images.png" alt="" class="copertina" />
				</li>
				<div class="info h-75 pt-5">
					<!-- titolo -->
					<li>Titolo: {{ result.name || result.title }}</li>
					<!-- titolo originale -->
					<li>
						Titolo originale:
						{{ result.original_name || result.original_title }}
					</li>
					<!-- lingua originale -->
					<li
						v-if="
							result.original_language == 'en' ||
								result.original_language == 'it'
						"
					>
						Lingua originale:
						<img
							class="flag-img ps-3"
							:src="require(`../assets/images/${result.original_language}.png`)"
							alt=""
						/>
					</li>
					<li v-else>Lingua oiginale: {{ result.original_language }}</li>
					<!-- voto -->
					<li>
						<div v-if="result.vote_average !== 0">
							<span v-for="(n, index) in 5" :key="`${n}-${index}`">
								<i v-if="starCount < index + 1" class="far fa-star"></i
								><i v-else class="fas fa-star"></i>
							</span>
						</div>
					</li>
					<li v-if="result.overview">Overview: {{ result.overview }}</li>
				</div>
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
	li {
		font-size: 20px;
		color: honeydew;
	}
	.flag-img {
		width: 100px;
	}

	.info {
		display: none;
		overflow: auto;
	}

	.hover-card:hover .info {
		display: flex;
		flex-direction: column;
		justify-content: space-around;
	}

	.hover-card:hover .copertina {
		display: none;
	}
}
</style>
