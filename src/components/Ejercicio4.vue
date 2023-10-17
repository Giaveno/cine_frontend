<template>
    <div>
        <h1>- Ejercicio 4, 5 y 6-</h1>
        <h2>Lista de compras: </h2>
    <div>
        <input v-model="nuevoItem" @keyup.enter="agregarItem" placeholder="Nombre del item" />
        <input v-model.number="cantidad" type="number" placeholder="Cantidad" />
        <button @click="agregarItem">Agregar</button>
    </div>

        <ul v-if="listaCompras.length > 0">
        <li v-for="item in listaCompras" :key="item.id">
            {{ item.nombre }} ({{ item.cantidad }} unidades)
            <button @click="deleteItem(item.id)">Eliminar</button>
        </li>
        </ul>
      
        <p v-else>No hay nada en la lista</p>
    </div>
</template>
  
<script>
export default {
data() {
    return {
    nuevoItem: '',
    cantidad: 1,
    listaCompras: [],
    };
},
methods: {
    agregarItem() {
    // Valido
    if (this.nuevoItem.trim() === '' || isNaN(this.cantidad) || this.cantidad <= 0) {
        alert('Ingrese un nombre de item válido y una cantidad válida (número mayor a cero).');
        return;
    }

    // Genero ID para el nuevo item a cargar
    const nuevoId = this.uuidv4();

    // Agrego item
    this.listaCompras.push({
        id: nuevoId,
        nombre: this.nuevoItem,
        cantidad: this.cantidad,
    });

    // Limpio
    this.nuevoItem = '';
    this.cantidad = 1;
    },
    deleteItem(itemId) {
    // Elimino por id
    this.listaCompras = this.listaCompras.filter((item) => item.id !== itemId);
    },
    uuidv4() {
    // Función para generar un UUID único
    return 'xxxxxxxx-xxxx-4xxx-yxxx-xxxxxxxxxxxx'.replace(/[xy]/g, function(c) {
        var r = Math.random() * 16 | 0, v = c == 'x' ? r : (r & 0x3 | 0x8);
        return v.toString(16);
    });
    },
},
};
</script>
  