<template>
    <div>
        <label>Nombre de la película: </label><input v-model="name">
        <label>Precio</label><input v-model="price">
        <button @click="agregarItem()">Agregar</button>
        <table>
            <tr>
                <th>Id</th>
                <th>Nombre</th>
                <th>Precio</th>
                <th>Proveedor</th>
            </tr>
            <tr v-for="item in items" :key="item.id">
                <td>{{ item.id }}</td>
                <td>{{ item.name }}</td>
                <td>{{ item.price }}</td>
                <td>{{ item.provider }}</td>
            </tr>
        </table>
    </div>
</template>

<script>
/* eslint-disable */
import axios from 'axios'

export default {
    name: 'APITest',
    data: function(){
        return {
            items: [],
            name: '',
            price: '',
        }
    },
    methods: {
        cargarDatos (){
            axios.get('http://localhost:8000/items/')
            .then(response => {
                this.items = response.data
                console.log(response.data)
            })
            .catch(error => {
                console.log(error)
            })
        },
        agregarItem(){
            axios.post('http://localhost:8000/items/', {
                name: this.name,
                price: this.price
            })
            .then(response => {
                console.log(response)
                this.cargarDatos()
            })
            .catch(error => {
                console.log(error)
            })
        }
    },
    mounted() {
        this.cargarDatos()
    }
}
</script>
  