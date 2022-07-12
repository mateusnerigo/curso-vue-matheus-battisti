<template>
	<div>
		<h2>O nome da pessoa é {{ nome }}</h2>

		<Info :email='email' :situacao='esta_trabalhando' />
		<Form />
	</div>
</template>

<script>
	import Info from './Info.vue';
	import Form from './Form.vue';

	export default {
		components: {
			Info,
			Form,
		},
		name: 'Pessoa',
		data() {
			return {
				nome: 'Mateus',
				email: 'mateus@email.com',
				esta_trabalhando: true,
			};
		},
	};
</script>

