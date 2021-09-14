<template>
	<div id="card" class="col col-md-6 col-xl-4">
		<ul class="h-100">
			<div class="hover-card h-100">
				<li v-if="item.poster_path">
					<img
						:src="`${imgBaseUrl}${item.poster_path}`"
						alt=""
						class="copertina"
					/>
				</li>
				<li v-else>
					<img src="../assets/images/images.png" alt="" class="copertina" />
				</li>
				<div class="info h-75 pt-5">
					<!-- titolo -->
					<li>Titolo: {{ item.name || item.title }}</li>
					<!-- titolo originale -->
					<li>
						Titolo originale:
						{{ item.original_name || item.original_title }}
					</li>
					<!-- lingua originale -->
					<li
						v-if="
							item.original_language == 'en' || item.original_language == 'it'
						"
					>
						Lingua originale:
						<img
							class="flag-img ps-3"
							:src="require(`../assets/images/${item.original_language}.png`)"
							alt=""
						/>
					</li>
					<li v-else>Lingua oiginale: {{ item.original_language }}</li>
					<!-- voto -->
					<li>
						<div v-if="item.vote_average !== 0">
							<span v-for="n in 5" :key="n">
								<i v-if="starCount < n" class="far fa-star"></i
								><i v-else class="fas fa-star"></i>
							</span>
						</div>
					</li>
					<li v-if="item.overview">Overview: {{ item.overview }}</li>
				</div>
			</div>
		</ul>
	</div>
</template>

<script>
export default {
	name: "Card",
	props: ["item"],
	data() {
		return {
			imgBaseUrl: "https://image.tmdb.org/t/p/w342",
		};
	},
	computed: {
		starCount() {
			const fiveCount = Math.ceil(this.item.vote_average / 2);
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
