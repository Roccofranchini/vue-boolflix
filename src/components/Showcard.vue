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
				<div class="info h-75 pt-5 mt-5">
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
					<button
						type="button"
						class="btn btn-light my-4 w-25"
						@click="moreInfo"
					>
						Cast
					</button>
					<ul v-if="cast.length > 0">
						CAST:
						<li v-for="(actor, index) in 5" :key="index">
							{{ cast[index].name }}
						</li>
					</ul>
				</div>
			</div>
		</ul>
	</div>
</template>

<script>
import axios from "axios";
export default {
	name: "Card",
	props: ["item", "endpoint"],
	data() {
		return {
			imgBaseUrl: "https://image.tmdb.org/t/p/w342",
			cast: [],
			endp: this.endpoint,
			itmId: this.item.id,
			genres: [],
		};
	},
	computed: {
		starCount() {
			const fiveCount = Math.ceil(this.item.vote_average / 2);
			return fiveCount;
		},
	},
	methods: {
		moreInfo() {
			axios
				.get(
					`https://api.themoviedb.org/3/${this.endp}/${this.itmId}/credits?api_key=e99307154c6dfb0b4750f6603256716d&language=it-IT`
				)
				.then((res) => {
					const cast = res.data.cast;
					this.cast = cast;
				});
		},
	},
};
</script>

<style scoped lang="scss">
#card {
	ul {
		color: honeydew;
	}
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
		align-items: center;
		justify-content: space-around;
	}

	.hover-card:hover .copertina {
		display: none;
	}
}
</style>
