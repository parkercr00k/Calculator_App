<template>
  <div id="app">
    <calculator-vue />
  </div>
</template>

<script>
import CalculatorVue from './components/Calculator.vue'

export default{
  components: { CalculatorVue },
  name: "app",
}
</script>


<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  text-align: center;
}
</style>
