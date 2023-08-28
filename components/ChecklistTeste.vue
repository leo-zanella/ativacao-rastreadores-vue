<template>
    <v-container class="justify-center">
      <v-card-text class="align-center d-flex">Selecione apenas o que está funcionando no veículo:</v-card-text>
      <v-checkbox
        v-model="checkboxes[0].value"
        :label="`Faróis`"
        color="green lighten-1"
      ></v-checkbox>
      <v-checkbox
        v-model="checkboxes[1].value"
        :label="`Limpador de para-brisa`"
        color="green lighten-1"
      ></v-checkbox>
      <v-checkbox
        v-model="checkboxes[2].value"
        :label="`Vidro elétrico`"
        color="green lighten-1"
      ></v-checkbox>
      <v-checkbox
        v-model="checkboxes[3].value"
        :label="`Tranca elétrica`"
        color="green lighten-1"
      ></v-checkbox>
      <v-checkbox
        v-model="checkboxes[4].value"
        :label="`Rádio`"
        color="green lighten-1"
      ></v-checkbox>
  
      <v-checkbox
        v-model="checkboxes[5].value"
        :label="`Alarme`"
        color="green lighten-1"
      ></v-checkbox>
    </v-container>
  </template>
  
  <script>
  export default {
  
    props: {
      exibirOverlay: {
        type: Boolean,
        default: false,
      },
    },
    data() {
      return {
        checkboxes: [
          { label: "Faróis", value: false },
          { label: "Limpador de para-brisa", value: false },
          { label: "Vidro elétrico", value: false },
          { label: "Tranca elétrica", value: false },
          { label: "Rádio", value: false },
          { label: "Alarme", value: false },
        ],
      };
    },
    
    watch: {
      checkboxes: {
        deep: true,
        handler() {
          this.emitirDadosCheckbox();
        },
      },
    },
  
  
    methods: {
      emitirDadosCheckbox() {
        this.$emit("dados-checkbox", this.checkboxes);
      },
      mounted() {
        this.emitirDadosCheckbox();
    },
    },
  };
  </script>