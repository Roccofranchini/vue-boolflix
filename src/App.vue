<template>
	<div id="app">
		<input type="text" v-model="query" />
		<button @click="search">cerca</button>
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
			apiData: [],
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
					this.apiData = datas;
				})
				.catch(() => {
					this.error = true;
				});
		},
	},
};
</script>

<style lang="scss">
#app {
	font-family: Avenir, Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;
	color: #2c3e50;
	margin-top: 60px;
}
</style>
