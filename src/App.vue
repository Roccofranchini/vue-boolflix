<template>
	<div id="app">
		<Search placeholder="cerca.." @search="search" />
		<ul>
			<Card v-for="result in results" :key="result.id" :result="result" />
		</ul>
	</div>
</template>

<script>
import axios from "axios";
import Card from "@/components/Card.vue";
import Search from "@/components/Search.vue";

export default {
	name: "App",
	components: {
		Card,
		Search,
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
body {
	text-align: center;
}
li {
	list-style-type: none;
}
</style>
