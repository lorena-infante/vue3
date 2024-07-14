<template>
    <div class="md:w-1/2">
        <h2 class="font-black text-3xl text-center">Seguimiento pacientes</h2>
        <p class="text-lg mt-5 text-center mb-10">
            Añade pacientes y <span class="text-indigo-600 text-bold">adminístralos</span>
        </p>
        <Alerta v-if="alerta.mensaje" :alerta="alerta" />
        <form @submit.prevent="validar" class="bg-white shadow-md rounded-lg py-10 px-5 mb-10">
            <div class="mb-5">
                <label for="mascota" class="block text-gray-700 uppercase font-bold">
                    Nombre Mascota
                </label>
                <input type="text" id="mascota" placeholder="Nombre de mascota"
                    class="border-2 w-full p-2 my-2 placeholder-gray-400 rounded-md" v-model="paciente.nombre" />

            </div>
            <div class="mb-5">
                <label for="propietario" class="block text-gray-700 uppercase font-bold">
                    Nombre Propietario
                </label>
                <input type="text" id="propietario" placeholder="Nombre del propietario"
                    class="border-2 w-full p-2 my-2 placeholder-gray-400 rounded-md" v-model="paciente.propietario" />
            </div>
            <div class="mb-5">
                <label for="email" class="block text-gray-700 uppercase font-bold">
                    Email
                </label>
                <input type="text" id="email" placeholder="Email"
                    class="border-2 w-full p-2 my-2 placeholder-gray-400 rounded-md" v-model="paciente.email" />
            </div>
            <div class="mb-5">
                <label for="alta" class="block text-gray-700 uppercase font-bold">
                    Fecha de alta
                </label>
                <input type="date" id="alta" placeholder="alta"
                    class="border-2 w-full p-2 my-2 placeholder-gray-400 rounded-md" v-model="paciente.alta" />
            </div>
            <div class="mb-5">
                <label for="sintomas" class="block text-gray-700 uppercase font-bold">
                    Síntomas
                </label>
                <textarea id="sintomas" placeholder="Describe los síntomas de tu mascota"
                    class="border-2 w-full p-2 my-2 placeholder-gray-400 rounded-md h-40" v-model="paciente.sintomas" />
            </div>
            <input type="submit"
                class="bg-indigo-600 w-full p-3 text-white uppercase font-bold hover:bg-indigo-700 cursor-pointer transition-colors"
                value="Registrar Paciente" />

        </form>

    </div>
</template>

<script setup>
import { reactive } from 'vue';
import Alerta from './Alerta.vue';

const alerta = reactive({
    mensaje: '',
    tipo: ''
})

const paciente = reactive({
    nombre: '',
    propietario: '',
    email: '',
    alta: '',
    sintomas: ''
})

const validar = () => {
    //validar values

    if (Object.values(paciente).includes('')) {
        alerta.mensaje = "Debe completar todos los campos";
        alerta.tipo = 'error'
        return;
    }
    alerta.mensaje = "Paciente agregado con éxito";
    alerta.tipo = 'exito'
}
</script>