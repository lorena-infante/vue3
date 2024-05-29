<script setup>
import { ref, reactive, onMounted, watch } from 'vue';
import { db } from './data/guitarras';
import Guitarra from './components/Guitarra.vue';
import Header from './components/Header.vue';
import Footer from './components/Footer.vue';

const guitarras = ref([]);
const carrito = ref([]);
const guitarra = ref([]);

watch(carrito, () => { guardarLS() },
    { deep: true }
);

onMounted(() => {
    guitarras.value = db;
    guitarra.value = db[3];

    const carritoStorage = localStorage.getItem('carrito');
    if (carritoStorage) {
        carrito.value = JSON.parse(carritoStorage);
    }

});

const guardarLS = () => {
    localStorage.setItem('carrito', JSON.stringify(carrito.value));
};

const agregarCarrito = (guitarra) => {
    const guitarExists = carrito.value.findIndex(el => el.id === guitarra.id);

    if (guitarExists >= 0) {
        carrito.value[guitarExists].cantidad++;
    } else {
        guitarra.cantidad = 1;
        carrito.value.push(guitarra);
    }
    guardarLS();

}
const decrementarCantidad = (id) => {
    const index = carrito.value.findIndex(el => el.id === id);
    if (carrito.value[index].cantidad > 1) {
        carrito.value[index].cantidad--;
    } else return;

    guardarLS();
}
const incrementarCantidad = (id) => {
    const index = carrito.value.findIndex(el => el.id === id);
    if (carrito.value[index].cantidad <= 4) {
        carrito.value[index].cantidad++;
    } else return;

    guardarLS();
}

const eliminarProducto = (id) => {
    carrito.value = carrito.value.filter(producto => producto.id !== id);
    guardarLS();
}

const vaciarCarrito = () => {
    carrito.value = [];
    guardarLS();
}

</script>


<template>
    <Header :guitarra="guitarra" :carrito="carrito" @agregar-carrito="agregarCarrito"
        @incrementar-cantidad="incrementarCantidad" @decrementar-cantidad="decrementarCantidad"
        @eliminar-producto="eliminarProducto" @vaciar-carrito="vaciarCarrito" />
    <main class="container-xl mt-5">
        <h2 class="text-center">Nuestra Colección</h2>
        <div class="row mt-5">
            <Guitarra v-for="guitarra in guitarras" :guitarra="guitarra" @agregar-carrito="agregarCarrito" />
        </div>
    </main>


    <Footer />
</template>