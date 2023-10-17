<template>
  <div>
    <h1>- Ejercicio 2 y 3 -</h1>
    <h2>Calculadora</h2>
    <div>
      <label for="numero1">Número 1:</label>
      <input type="text" id="numero1" v-model="numero1" />
    </div>
    <div>
      <label for="numero2">Número 2:</label>
      <input type="text" id="numero2" v-model="numero2" />
    </div>
    <div>
      <label for="operacion">Operación:</label>
      <select id="operacion" v-model="selectedOperation">
        <option value="suma">Suma</option>
        <option value="resta">Resta</option>
        <option value="multiplicacion">Multiplicación</option>
        <option value="division">División</option>
      </select>
    </div>
    <button @click="calcularResultado">Calcular</button>
    <div class="resultado">
      <p>Resultado: {{ resultado }}</p>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      numero1: '0',
      numero2: '0',
      selectedOperation: 'suma',
      resultado: 0
    }
  },
  methods: {
    calcularResultado () {
      const num1 = parseFloat(this.numero1)
      const num2 = parseFloat(this.numero2)

      if (!isNaN(num1) && !isNaN(num2)) {
        if (this.selectedOperation === 'suma') {
          this.resultado = num1 + num2
        } else if (this.selectedOperation === 'resta') {
          this.resultado = num1 - num2
        } else if (this.selectedOperation === 'multiplicacion') {
          this.resultado = num1 * num2
        } else if (this.selectedOperation === 'division') {
          if (num2 !== 0) {
            this.resultado = num1 / num2
          } else {
            this.resultado = 'Error --> División por cero'
          }
        }
      } else {
        this.resultado = 'Error --> Ingresa números válidos'
      }
    }
  }
}
</script>

<style>
  .resultado{
      color: green;
      font-size: 2em;
      font-weight: bold;
  }
</style>
