<script setup>
import { ref, reactive, onMounted } from 'vue';
import { db } from './data/guitarras';
import Guitarra from './components/Guitarra.vue';
import Header from './components/Header.vue';
import Footer from './components/Footer.vue';

const guitarras = ref([]);
const carrito = ref([]);

onMounted(() => {
    guitarras.value = db;
    console.log(guitarras.value);

});
const agregarCarrito = (guitarra) => {
    const guitarExists = carrito.value.findIndex(el => el.id === guitarra.id);

    if (guitarExists >= 0) {
        carrito.value[guitarExists].cantidad++;
    } else {
        guitarra.cantidad = 1;
        carrito.value.push(guitarra);
    }
}

</script>


<template>
    <Header :carrito="carrito" />
    <main class="container-xl mt-5">
        <h2 class="text-center">Nuestra Colección</h2>
        <div class="row mt-5">
            <Guitarra v-for="guitarra in guitarras" :guitarra="guitarra" @agregar-carrito="agregarCarrito" />
        </div>
    </main>


    <Footer />
</template>