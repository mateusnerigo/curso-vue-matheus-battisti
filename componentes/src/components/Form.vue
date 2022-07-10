<template>
  <div>
    <h2>Meu Formulário: </h2>
    <form action="" @submit='enviarFormulario($event)'>
      <div>
        <label>Nome </label>
        <input type="text" v-model='name'>
      </div>

      <div>
        <label>Email </label>
        <input type="text" v-model='email'>
      </div>

      <Submit />
    </form>
  </div>
</template>

<script>
import InputText from './form/InputText.vue';
import Submit from './form/Submit.vue';

export default {
  name: 'Form',
  components: {
    InputText,
    Submit
  },
  data() {
    return {
      name: '',
      email: ''
    }
  },
  methods: {
    enviarFormulario(e) {
      e.preventDefault();

      const name = this.name;
      const email = this.email;

      console.log('Formulário enviado!');
      console.log(`Nome: ${name}`);
      console.log(`Email: ${email}`);
    }
  }
}
</script>

<style scoped>
  p {
    margin: 50px;
  }
</style>
