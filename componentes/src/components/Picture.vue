<template>
	<div>
		<img :src="avatar" :alt="description">
		<MudarImagem @mudar-imagem="mudarImagem" />
	</div>
</template>

<script>
	import MudarImagem from './MudarImagem.vue';

	export default {
		name: 'Picture',
		components: {
			MudarImagem,
		},
		data() {
			return {
				avatar: 'https://picsum.photos/200',
				description: 'Mateus Neri',
			};
		},
		methods: {
			mudarImagem() {
				this.avatar = 'https://picsum.photos/200/200';
			},
		},
	};
</script>
