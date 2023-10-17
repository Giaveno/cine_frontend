<template>
    <div class="nombre-container">
        <h1>- Ejercicio 1 -</h1>
        <h2>Ingrese su nombre:</h2>
        <input v-model="nombre" class="nombre-input">
        <p>Usted se llama: <span class="nombre">{{ nombre }}</span></p>
    </div>
</template>

<script>
export default {
  name: 'Main',
  data: function () {
    return {
      nombre: ''
    }
  }
}
</script>

<style>
.nombre-container {
  text-align: center;
  margin: 20px;
}

.nombre-input {
  width: 20%;
  padding: 10px;
  font-size: 16px;
  margin-top: 10px;
}

.nombre {
  font-size: 18px;
  font-weight: bold;
  color: #007bff;
}
</style>
