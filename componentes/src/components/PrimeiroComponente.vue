<template>
	<div>
		<h1>Yo, Vue component!</h1>
		<p>Username: {{ nickname }}</p>
		<p>Role: {{ role }}</p>

		<MultiplosEventos />
		<Reutilizacao />
		<Reutilizacao />
		<Reutilizacao />
		<Reutilizacao />
		<Reutilizacao />
		<Reutilizacao />
		<Reutilizacao />
	</div>
</template>

<script>
import MultiplosEventos from './MultiplosEventos.vue';
import Reutilizacao from './Reutilizacao.vue';

export default {
  name: "PrimeiroComponente",
	components: {
		MultiplosEventos,
		Reutilizacao
	},
  data() {
		return {
			nickname: "mateusNeriGo",
			role: "Programmer"
		}
	},
};
</script>
