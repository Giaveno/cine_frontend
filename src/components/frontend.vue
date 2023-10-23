<template>
    <div>
        <label for="movieSelect">Selecciona una película:</label>
        <select v-model="selectedMovie" id="movieSelect">
            <option v-for="movie in movies" :key="movie.id" :value="movie.id">{{ movie.name }}</option>
        </select>

        <div v-if="selectedMovie">
            <h2>Funciones disponibles para {{ selectedMovieName }}</h2>
            <ul>
                <li v-for="functionItem in functions" :key="functionItem.id">
                    {{ functionItem.date }} - Sala {{ functionItem.hall.name }}
                    <button @click="verAsientos(functionItem.id)">Seleccionar</button>
                </li>
            </ul>
        </div>

        <div v-if="selectedFunction">
            <h2>Asientos Libres para {{ selectedFunctionDate }} - Sala {{ selectedFunctionHall }}</h2>
            <label for="seatSelect">Selecciona un asiento:</label>
            <select v-model="selectedSeatId" id="seatSelect">
                <option value="" disabled>-- Selecciona un asiento --</option>
                <option v-for="seat in availableSeats" :key="seat.id" :value="seat.id">{{ seat.number }}</option>
            </select>
            <button @click="guardarInformacion">Guardar</button>
        </div>


        <div v-if="ticketGuardado">
            <h2>Tu información ha sido guardada.</h2>
        </div>
    </div>
</template>
  
<script>
import axios from 'axios';

export default {
    name: 'ReservaBoleto',
    data() {
        return {
            movies: [],
            functions: [],
            availableSeats: [],
            selectedMovie: null,
            selectedMovieName: '',
            selectedFunction: null,
            selectedFunctionDate: '',
            selectedFunctionHall: '',
            selectedSeatId: null,
            ticketGuardado: false,
        };
    },
    methods: {
        cargarPeliculas() {
            axios.get('http://localhost:8000/api/movies/')
                .then(response => {
                    this.movies = response.data;
                })
                .catch(error => {
                    console.log(error);
                });
        },
        cargarFunciones(movieId) {
            axios.get(`http://localhost:8000/api/functions/?movie=${movieId}`)
                .then(response => {
                    this.functions = response.data;
                })
                .catch(error => {
                    console.log(error);
                });
        },
        verAsientos(functionId) {
            axios.get(`http://localhost:8000/api/seats/?function=${functionId}&is_booked=false`)
                .then(response => {
                    this.availableSeats = response.data;
                    this.selectedFunction = functionId;
                    this.selectedSeatId = null; // Reiniciar la selección de asiento
                    this.ticketGuardado = false;
                })
                .catch(error => {
                    console.log(error);
                });
        },
        seleccionarAsiento(seatId) {
            this.selectedSeatId = seatId;
        },
        guardarInformacion() {
            if (this.selectedFunction && this.selectedSeatId) {
                const reserva = {
                    function: this.selectedFunction,
                    seat: this.selectedSeatId,
                };

                axios.post('http://localhost:8000/api/tickets/', reserva) // Asumiendo que tienes una ruta /api/tickets/ en tu backend para crear tickets
                    .then(response => {
                        console.log(response);
                        this.ticketGuardado = true;
                    })
                    .catch(error => {
                        console.error(error);
                    });
            }
        }
    },
    watch: {
        selectedMovie(newVal) {
            this.selectedMovieName = newVal ? this.movies.find(movie => movie.id === newVal).name : '';
            this.selectedFunction = null;
            this.availableSeats = [];
            this.selectedSeatId = null; // Reiniciar la selección de asiento
            this.ticketGuardado = false;
            if (newVal) {
                this.cargarFunciones(newVal);
            }
        }
    },
    mounted() {
        this.cargarPeliculas();
    },
};
</script>
  