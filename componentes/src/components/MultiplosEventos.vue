<template>
  <div>
    <button @click='primeiroEvento(txt1, $event), segundoEvento(txt2, $event)'>Ativar múltiplos eventos</button>
    <p>{{ multiplos_eventos }}</p>
  </div>
</template>

<script>
export default {
  name: 'MultiplosEventos',
  data() {
    return {
      multiplos_eventos: '',
      txt1: 'Primeiro Evento!',
      txt2: 'Segundo Evento!',
    }
  },
  methods: {
    primeiroEvento(txt, e) {
      this.multiplos_eventos = txt;
    },
    segundoEvento(txt, e) {
      setTimeout(() => this.multiplos_eventos = txt, 500)
    }
  }
}
</script>

<style scoped>
  div {
    margin: 100px;
  }
</style>
