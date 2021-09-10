<template>
	<div id="app">
		<input type="text" v-model="query" />
		<button @click="search">cerca</button>
		<ul>
			<Card v-for="(result, index) in results" :key="index" :result="result" />
		</ul>
	</div>
</template>

<script>
import axios from "axios";
import Card from "@/components/Card.vue";

export default {
	name: "App",
	components: {
		Card,
	},
	data() {
		return {
			query: "",
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
			axios
				.get(
					`${this.baseUri}/search/tv?api_key=${this.apiKey}&query=${this.query}`
				)
				.then((res) => {
					const datas = res.data.results;
					this.tvs = datas;
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
