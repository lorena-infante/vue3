<template>
  <div class="container mx-auto mt-20">
    <Header />
    <div class="mt-12 md:flex">
      <Formulario v-model:nombre="paciente.nombre" v-model:propietario="paciente.propietario"
        v-model:email="paciente.email" v-model:alta="paciente.alta" v-model:sintomas="paciente.sintomas" />
      <div class="md:w-1/2 md:h-screen overflow-y-scroll">
        <h3 class="font-black text-3xl text-center">Administra tus pacientes</h3>
        <div v-if="pacientes.length > 0">

        </div>
        <p v-else class="mt-20 text-2xl text-center">
          No hay pacientes registrados

        </p>
      </div>
    </div>
  </div>
</template>

<script setup>
import Header from './components/Header.vue';
import Formulario from './components/Formulario.vue';
import { ref, reactive } from 'vue';

const pacientes = ref([]);
const paciente = reactive({
  nombre: '',
  propietario: '',
  email: '',
  alta: '',
  sintomas: ''
})

</script>