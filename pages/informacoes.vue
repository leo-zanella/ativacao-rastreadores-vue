<template>
    <main class="d-flex align-center flex-column">
   <h2 class="mt-5">Informações</h2>
      <v-card
        elevation="0"
        width="95%"
        max-width="750px"
        color="grey lighten-2"
        height="100px"
        class="ma-3 d-flex flex-column justify-center align-center"
      >
      <span>Tipo:</span>
      <h2 class="font-weight-bold" >Instalação</h2>
    
      <span>Opcionais: Buzzer; Bloqueio .</span>
    </v-card>

    <v-card
        elevation="0"
        width="95%"
        max-width="750px"
        color="grey lighten-2"
        height="300px"
        class="ma-3 d-flex flex-column justify-center align-left"
      >
      <v-card-subtitle>Prestador:</v-card-subtitle>
      <v-card-subtitle>Cliente:</v-card-subtitle>
      <v-card-subtitle>Contato do cliente:</v-card-subtitle>
      <v-card-subtitle>Endereço:</v-card-subtitle>
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