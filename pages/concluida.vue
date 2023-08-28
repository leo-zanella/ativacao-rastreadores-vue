<template>
    <div>
      <v-card-title class="align-center justify-center ">Instalação Concluída!</v-card-title>
      <check-animation></check-animation>
    </div>
  </template>
  
  <script>
  import CheckAnimation from '~/components/CheckAnimation.vue';
  
  export default {
    components: {
      CheckAnimation,
    },
  };
  </script>
  