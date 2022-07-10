<template>
  <div>
    <p v-if='esta_trabalhando'>Estou trabalhando no momento.</p>
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
  components: {
    Picture
  },
  name: 'Info',
  data() {
    return {
      esta_trabalhando: true,
      mostrar_email: false,
      texto_botao: 'Mostrar email',
      backend_technologies: ['JS', 'PHP', 'Java'],
      frontend_technologies: [
        {id: 1, language: 'Bootstrap'},
        {id: 2, language: 'VueJS'},
        {id: 3, language: 'SCSS'},
      ],

      email: 'mateus@email.com',
      link_portfolio: 'https://google.com'
    }
  },
  methods: {
    showEmail() {
      const mostrarEmail = this.mostrar_email;
      mostrarEmail = !mostrarEmail;
      this.texto_botao = (!mostrarEmail)
        ? 'Mostrar email'
        : 'Esconder email';
    }
  }
}
</script>
