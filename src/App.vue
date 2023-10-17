<template>
  <div id="app">
    <label for="SelectorEJ">Selecciona un ejercicio:</label>
    <select id="SelectorEJ" v-model="selectedEj">
      <option value="ejercicio1">Ejercicio 1</option>
      <option value="ejercicio2">Ejercicio 2 y 3</option>
      <option value="ejercicio4">Ejercicio 4, 5 y 6</option>
      <option value="frontend">front</option>
    </select>

    <component :is="selectedEj" />

  </div>
</template>

<script>
import Ejercicio1 from './components/Ejercicio1'
import Ejercicio2 from './components/Ejercicio2'
import Ejercicio4 from './components/Ejercicio4'
import frontend from './components/frontend.vue'

export default {
  name: 'App',
  components: {
    Ejercicio1,
    Ejercicio2,
    Ejercicio4,
    frontend
  },
  data () {
  return {
    selectedEj: 'ejercicio1'
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
