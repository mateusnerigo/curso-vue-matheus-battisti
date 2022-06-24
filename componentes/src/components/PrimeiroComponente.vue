<template>
	<div>
		<h1>Yo, Vue component!</h1>
		<p>Username: {{ nickname }}</p>
		<p>Role: {{ role }}</p>
	</div>
</template>

<script>
export default {
  name: "PrimeiroComponente",
  data() {
		return {
			nickname: "mateusNeriGo",
			role: "Programmer"
		}
	},
};
</script>
