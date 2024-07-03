<template>
    <div class="min-h-screen flex items-start md:items-center justify-center">
      <div class="max-w-md w-full p-6 rounded-lg md:shadow-2xl mt-8 md:mt-0">
        <h2 class="text-center text-2xl font-bold mb-4 text-black">Calculadora de daño</h2>
        <div class="grid grid-cols-1 gap-4">
          <input class="bg-gray-600 hover:bg-gray-500 outline-none h-10 rounded pl-2 w-full text-white font-medium" type="text" v-model="ataque" @input="validarEntrada($event, false)" placeholder="Ingresá cuanto daño hiciste" id="ataque" autocomplete="off">
          <input class="bg-gray-600 hover:bg-gray-500 outline-none h-10 rounded pl-2 w-full text-white font-medium" type="text" v-model="defensa" @input="validarEntrada($event, false)" placeholder="Ingresá la defensa del enemigo" id="defensa" autocomplete="off">
          <input class="bg-gray-600 hover:bg-gray-500 outline-none h-10 rounded pl-2 w-full text-white font-medium" type="text" v-model="probabilidad" @input="validarEntrada($event, true)" placeholder="Ingresá el % de aumento de daño" id="probabilidad" autocomplete="off">
          <span class="text-xl font-bold text-black">Daño: {{ daño }}</span>
        </div>
        <div class="grid grid-cols-2 gap-4 mt-4">
          <button class="rounded p-2 bg-blue-500 hover:bg-blue-600 text-white" @click="calcularDaño">Calcular Daño</button>
          <button class="rounded p-2 bg-red-600 hover:bg-red-500 text-white" @click="resetCampos">Reset</button>
        </div>
      </div>
    </div>
  </template>

<script>
import { ref } from 'vue';

export default {
  name: 'Calculadora',
  setup() {
    const ataque = ref('');
    const defensa = ref('');
    const probabilidad = ref('');
    const daño = ref(0);

    const validarEntrada = (event, isPercentage) => {
      const input = event.target;
      input.value = input.value.replace(/[^0-9]/g, '').slice(0, isPercentage ? 3 : 2);
      if (isPercentage) {
        probabilidad.value = input.value;
      } else {
        if (input.id === 'ataque') {
          ataque.value = input.value;
        } else {
          defensa.value = input.value;
        }
      }
    };

    const calcularDaño = () => {
      if (ataque.value === '' || defensa.value === '' || probabilidad.value === '') {
        alert('Por favor, ingrese valores válidos para ataque, defensa y probabilidad.');
        return;
      }
      let resultado = ataque.value - (defensa.value * 0.6);
      const incremento = resultado * (probabilidad.value / 100);
      resultado = Math.round(resultado + incremento);
      if (resultado < 0) {
        resultado = 0;
      }
      daño.value = resultado;
    };

    const resetCampos = () => {
      ataque.value = '';
      defensa.value = '';
      probabilidad.value = '';
      daño.value = 0;
    };

    return {
      ataque,
      defensa,
      probabilidad,
      daño,
      validarEntrada,
      calcularDaño,
      resetCampos,
    };
  },
};
</script>
  
  <style scoped>
  input::placeholder {
  @apply text-gray-200; /* Aplica padding horizontal */
}
  </style>
  