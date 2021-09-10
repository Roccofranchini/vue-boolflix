<template>
	<div id="app">
		<input type="text" v-model="query" />
		<button @click="search">cerca</button>
		<ul>
			<ul v-for="film in films" :key="film.id">
				<li>{{ film.title }}</li>
				<li>{{ film.original_title }}</li>
				<li>{{ film.original_language }}</li>
				<li>{{ film.vote_average }}</li>
			</ul>
		</ul>
	</div>
</template>

<script>
import axios from "axios";

export default {
	name: "App",
	components: {},
	data() {
		return {
			query: "",
			baseUri: "https://api.themoviedb.org/3",
			apiKey: "561cc2175a0ff92f89627792016b88c4",
			films: [],
		};
	},
	methods: {
		search() {
			axios
				.get(
					`${this.baseUri}/search/movie?api_key=${this.apiKey}&query=${this.query}`
				)
				.then((res) => {
					const datas = res.data.results;
					this.films = datas;
				})
				.catch(() => {});
		},
	},
};
</script>

<style lang="scss">
body {
	text-align: center;
}
li {
	list-style-type: none;
}
</style>
