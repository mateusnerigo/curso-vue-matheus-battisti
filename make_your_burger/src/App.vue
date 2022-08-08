<template>
	<div>
		<Navbar :logo="logo_src" :alt="app_name" />
		<router-view />
		<Footer />
	</div>
</template>

<script>
	import Navbar from './components/Navbar.vue';
	import Footer from './components/Footer.vue';

	export default {
		name: 'App',
		components: {
			Navbar,
			Footer,
		},
		data() {
			return {
				logo_src: '/img/logo.png',
				app_name: 'Make your burger',
			};
		},
	};
</script>

<style>
	* {
		font-family: Helvetica, sans-serif;
		margin: 0;
		padding: 0;
		box-sizing: border-box;
	}

	.main-container {
		margin: 50px;
		min-height: 250px;
	}

	h1 {
		text-align: center;
		font-size: 42px;
		margin-bottom: 30px;
		color: #222;
	}
</style>
