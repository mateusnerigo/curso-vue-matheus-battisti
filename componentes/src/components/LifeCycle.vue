<template>
  <p>My name is: {{ name }}</p>
</template>

<script>
export default {
  name: "LifeCycle",
  data() {
    return {
      name: 'Ainda não sei'
    }
  },
  created() {
    setTimeout(() => {
      this.name = "Mateus"
    }, 1000);
  },
  mounted() {
    setTimeout(() => {
      this.name = "Doido"
    }, 2000)
  }
};
</script>
