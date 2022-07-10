<template>
  <div>
    <Header />
    <PrimeiroComponente />
    <p>------- {{ endText }} --------</p>

    <LifeCycle />
    <p>------- {{ endText }} --------</p>

    <Pessoa />
  </div>
</template>

<script>
import Header from "./components/Header";
import PrimeiroComponente from "./components/PrimeiroComponente";
import LifeCycle from "./components/LifeCycle"
import Pessoa from './components/Pessoa.vue';

export default {
  name: "App",
  components: {
    Header,
    PrimeiroComponente,
    LifeCycle,
    Pessoa,
  },
  data() {
    return {
      endText: "END"
    }
  }
};
</script>

<style>
  body {
    background-color: #666;
    color: #ccc;
  }

  a {
    color: #c77;
  }
</style>

