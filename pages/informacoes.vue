<template>
    <main class="d-flex align-center flex-column">
   <h2  class="mt-5 mb-5">Informações</h2>
      <v-card
        elevation="5"
        width="95%"
        max-width="750px"
        color="grey lighten-2"
        height="120px"
        class="ma-3 d-flex flex-column align-center mb-5">
      <v-card-subtitle class="mt-2 pb-0">Tipo:</v-card-subtitle>
      <v-card-title class="font-weight-bold pt-0" >Instalação </v-card-title>
      <v-card-subtitle v-if="opcional"> Opcionais: Buzzer; Bloqueio . </v-card-subtitle>
    </v-card>

    <v-card
        elevation="5"
        width="95%"
        max-width="750px"
        color="grey lighten-2"
        height="300px"
        class="ma-3 d-flex p-5 flex-column justify-center align-left"
      >
      <v-card-subtitle>Prestador: {{  }}</v-card-subtitle>
      <v-card-subtitle>Cliente: {{  }}</v-card-subtitle>
      <v-card-subtitle>Contato do cliente: {{  }}</v-card-subtitle>
      <v-card-subtitle>Endereço: {{  }}</v-card-subtitle>
    </v-card>
    <v-container class="d-flex justify-end">
      <v-btn
      text
      @click="redirectToVisitasAgendadas" 
      >
      Voltar
    </v-btn>
    <v-btn
      dark
      color="green darken-2"
      @click="redirectToOrdemDeServico()"
    >
      Confirmar
    </v-btn>
    </v-container>
  </main>
</template>

<script>
export default {

  data(){
    return{
    opcional: true,
    }
  },

  methods: {
      redirectToOrdemDeServico() {
        this.$router.push('/os');
      },
      redirectToVisitasAgendadas() {
        this.$router.push('/');
      }
    }

}
</script>

<style>

</style>