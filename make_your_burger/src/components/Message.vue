<template>
	<div class="message-container">
		<p>{{ msg }}</p>
	</div>
</template>

<script>
	export default {
		name: 'Message',
		props: {
			msg: String,
		},
	};
</script>

<style scoped>
	.message-container {
		color: #048;
		background-color: #cef;
		border: 2px solid #bdf;
		border-radius: 5px;
		padding: 10px;
		max-width: 400px;
		margin: 30px auto;
	}
</style>
