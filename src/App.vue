<template>
  <div id="app" class="bg-gray-100">
    <Header />
    <Calculadora />
  </div>
</template>

<script>
import Header from './components/Header.vue';
import Calculadora from './components/Calculadora.vue';

export default {
  name: 'App',
  components: {
    Calculadora,
    Header
  },
};
</script>

<style>
/* estilos globales si es necesario */
</style>
