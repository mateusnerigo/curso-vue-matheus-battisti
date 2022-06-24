<template>
  <div>
    <PrimeiroComponente />
    <p>------- {{ endText }} --------</p>

    <LifeCycle />
  </div>
</template>

<script>
import PrimeiroComponente from "./components/PrimeiroComponente";
import LifeCycle from "./components/LifeCycle"

export default {
  name: "App",
  components: {
    PrimeiroComponente,
    LifeCycle,
  },
  data() {
    return {
      endText: "END"
    }
  }
};
</script>

