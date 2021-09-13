<template>
	<header>
		<div class="row justify-content-between align-items-center h-100">
			<div class="col d-flex justify-content-start">
				<span class="logo px-5">BOOLFLIX</span>
			</div>
			<div class="col d-flex justify-content-end">
				<Search placeholder="cerca.." @search="search" class="px-5" />
			</div>
		</div>
	</header>
</template>

<script>
import Search from "./Search.vue";
export default {
	name: "Header",
	components: {
		Search,
	},
	methods: {
		search(search) {
			this.$emit("search", search);
		},
	},
};
</script>

<style scoped lang="scss">
header {
	height: 80px;
	background: grey;
	.logo {
		font-size: 40px;
		color: red;
		font-weight: bold;
	}
}
</style>
