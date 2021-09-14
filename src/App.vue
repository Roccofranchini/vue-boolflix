<template>
	<div id="app">
		<Header @search="search" />
		<Results
			v-if="this.films.length > 0"
			:items="films"
			title="FILM"
			endpoint="movie"
		/>
		<Results
			v-if="this.tvs.length > 0"
			:items="tvs"
			title="SERIE TV"
			endpoint="tv"
		/>
	</div>
</template>

<script>
import axios from "axios";
import Header from "@/components/Header.vue";
import Results from "@/components/Results.vue";

export default {
	name: "App",
	components: {
		Header,
		Results,
	},
	data() {
		return {
			baseUri: "https://api.themoviedb.org/3",
			apiKey: "561cc2175a0ff92f89627792016b88c4",
			films: [],
			tvs: [],
		};
	},
	computed: {
		results() {
			const result = [...this.films, ...this.tvs];
			return result;
		},
	},
	methods: {
		search(query) {
			if (!query) {
				this.tvs = this.films = [];
				return;
			}

			this.callApi(query, "search/movie", "films");
			this.callApi(query, "search/tv", "tvs");
		},
		callApi(query, endpoint, type) {
			const params = {
				params: {
					query,
					api_key: this.apiKey,
					language: "it-IT",
				},
			};
			axios
				.get(`${this.baseUri}/${endpoint}`, params)
				.then((res) => {
					this[type] = res.data.results;
				})
				.catch(() => {});
		},
	},
};
</script>

<style lang="scss">
@import "~bootstrap/scss/bootstrap.scss";

body {
	text-align: center;
}
#app {
	li {
		list-style-type: none;
	}
}
</style>
