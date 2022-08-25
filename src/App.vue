<template >
  <div>
    <Calculator msg="Calculadora" />
  </div>
</template>

<script>
import Calculator from './components/Calculator.vue';

export default {
  name: 'App',
  components: {
    Calculator
  }
}
</script>

<style>
body {
  /* background: rgba(#7f8c8d, 0.2) !important; */
  background: #cdcccd !important;
}
</style>
