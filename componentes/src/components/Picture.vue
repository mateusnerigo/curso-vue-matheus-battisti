<template>
  <img :src="avatar" :alt="description">
</template>

<script>
  export default {
    name: 'Picture',
    data() {
      return {
        avatar: 'https://picsum.photos/200',
        description: 'Mateus Neri'
      }
    }
  }
</script>
