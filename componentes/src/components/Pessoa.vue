<template>
  <div>
    <h2>O nome da pessoa é {{ nome }}</h2>

    <Info />
  </div>
</template>

<script>
  import Info from './Info.vue';
  
  export default {
    components: { Info },
    name: 'Pessoa',
    data() {
      return {
        nome: 'Mateus'
      }
    }
  }
</script>

