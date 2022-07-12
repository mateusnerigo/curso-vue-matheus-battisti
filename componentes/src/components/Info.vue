<template>
	<div>
		<p v-if='situacao'>Estou trabalhando no momento.</p>
		<p v-else>Estou em busca de novas oportunidades.</p>

		<p>Utilizo as seguintes tecnologias para backend: </p>
		<ul>
			<li v-for='(technology, index) in backend_technologies' :key='index'>
				{{ technology }}
			</li>
		</ul>

		<p>Utilizo as seguintes tecnologias para frontend:</p>
		<ul>
			<li v-for='technology in frontend_technologies' :key='technology.id'>
				{{ technology.language }}
			</li>
		</ul>

		<div>
			<button @click='showEmail'>{{ texto_botao }}</button>
		</div>

		<p v-show='mostrar_email'>Mande uma mensagem para {{ email }}</p>
		<p>Para acessar meu portfólio basta
			<a v-bind:href='link_portfolio' target="_blank">clicar aqui!</a>
		</p>

		<Picture />
	</div>
</template>

<script>
	import Picture from './Picture.vue';

	export default {
		name: 'Info',
		components: {
			Picture,
		},
		props: {
			email: String,
			situacao: Boolean,
		},
		data() {
			return {
				mostrar_email: false,
				texto_botao: 'Mostrar email',
				backend_technologies: ['JS', 'PHP', 'Java'],
				frontend_technologies: [
					{ id: 1, language: 'Bootstrap' },
					{ id: 2, language: 'VueJS' },
					{ id: 3, language: 'SCSS' },
				],

				link_portfolio: 'https://google.com',
			};
		},
		methods: {
			showEmail() {
				this.mostrar_email = !this.mostrar_email;
				this.texto_botao = !this.mostrar_email
					? 'Mostrar email'
					: 'Esconder email';
			},
		},
	};
</script>
