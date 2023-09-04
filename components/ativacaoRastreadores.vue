<template>
    <div class="fill-height d-flex flex-column justify-center align-center">
  
      <h2 class="align-center justify-center d-flex">Ativação do Rastreador</h2>
  
      <v-col md="4">
  
        <v-card height="180" class="pa-2 d-flex align-center flex-column">
          <v-card-title >Status da alimentação:</v-card-title>
            <v-icon large class="ma-2" :color="getAlimentacaoIconColor()">{{'mdi-lightning-bolt'}}</v-icon>
            <v-container class="d-flex text-center justify-center">
              {{ alimentacao ? 'O rastreador está conectado' : 'Rastreador desconectado' }}
            </v-container>
            </v-card>
      </v-col>
  
      <v-col md="4">
        
        <v-card height="180" class="pa-2 d-flex align-center flex-column">
          <v-card-title>Status da Ignição</v-card-title>
            <v-icon large class="ma-2" :color="getIgnicaoIconColor()">{{'mdi-key-variant'}}</v-icon>
              {{ ignicao ? 'Veículo ligado' : 'Veículo desligado' }}
        </v-card>
      </v-col>
  
      <v-col md="4">
  
      <v-card height="180" class="pa-1 d-flex align-center flex-column">
        <v-card-title>Bloqueio</v-card-title>
        <v-icon class="mb-2" large :class="getBloqueioIconClass()">{{ getBloqueioIcon() }}</v-icon>
          <v-btn v-if="!saida1.checked" class="mt-2" @click="ativarSaida(1)">Ativar</v-btn>
          <v-btn v-else-if="saida1.checked && !saida1.tested" class="mt-2" @click="testarSaida(1)">Testar Saída 1</v-btn>
          <v-btn v-else-if="saida1.checked && saida1.tested && !saida1.worked" class="mt-2" @click="testarSaida(1)">Reenviar Comando</v-btn>
          <v-btn v-else-if="saida1.checked && saida1.tested && saida1.worked" class="mt-2" @click="desativarSaida(1)">Desativar Saída 1</v-btn>
        </v-card>
      </v-col>
  
      <v-col md="4">
  
      <v-card height="180" class="pa-1 d-flex align-center flex-column">
        <v-card-title>Buzzer</v-card-title>
        <v-icon class="mb-2" x-large :color="getBuzzerIconClass()" >{{'mdi-whistle'}}</v-icon>
        <v-btn v-if="!saida2.checked" class="mt-2" @click="ativarSaida(2)" > Ativar </v-btn>
        <v-btn v-else-if="saida2.checked && !saida2.tested" class="mt-2" @click="testarSaida(2)">Testar Saída 2</v-btn>
        <v-btn v-else-if="saida2.checked && saida2.tested && !saida2.worked" class="mt-2" @click="testarSaida(2)">Reenviar Comando</v-btn>
        <v-btn v-else-if="saida2.checked && saida2.tested && saida2.worked" class="mt-2" @click="desativarSaida(2)">Desativar Saída 2</v-btn>
      </v-card>
  
      </v-col>
    </div>
    </template>
  
  <script>
  export default {
    data() {
      return {
        alimentacao: true,
        ignicao: true,
        saida1: {
          checked: false,
          tested: false,
          worked: false,
        },
        saida2: {
          checked: false,
          tested: false,
          worked: false,
        },
      };
    },
    methods: {
      getBuzzerIconClass(){
        return this.saida2.checked ? 'blue' : 'grey';
      },
      getBloqueioIcon() {
        return this.saida1.checked ? 'mdi-lock' : 'mdi-lock-open';
      },
  
      getBloqueioIconClass() {
        return this.saida1.checked ? 'red--text' : 'grey--text';
      },
      
      getAlimentacaoIconColor() {
        return this.alimentacao ? 'green' : 'grey';
      },
  
      getIgnicaoIconColor(){
        return this.ignicao ? 'green' : 'grey';
      },
  
      ativarSaida(saida) {
        if (saida === 1) {
          this.saida1.checked = true;
          this.saida1.tested = false;
          this.saida1.worked = false;
        } else if (saida === 2) {
          this.saida2.checked = true;
          this.saida2.tested = false;
          this.saida2.worked = false;
        }
      },
      testarSaida(saida) {
        // Aqui você pode adicionar a lógica para verificar se a saída funcionou fisicamente
        // Por exemplo, enviar um sinal para o dispositivo externo e aguardar uma resposta
        // Se funcionou, defina a propriedade "worked" como true
        // Se não funcionou, defina a propriedade "worked" como false
  
        if (saida === 1) {
          this.saida1.tested = true;
          this.saida1.worked = true; // Defina como true ou false com base na resposta real
        } else if (saida === 2) {
          this.saida2.tested = true;
          this.saida2.worked = true; // Defina como true ou false com base na resposta real
        }
      },
      reenviarComando(saida) {
        if (saida === 1) {
          this.saida1.checked = false;
          this.saida1.tested = false;
          this.saida1.worked = false;
          this.ativarSaida(1);
        } else if (saida === 2) {
          this.saida2.checked = false;
          this.saida2.tested = false;
          this.saida2.worked = false;
          this.ativarSaida(2);
        }
      },
      desativarSaida(saida) {
        if (saida === 1) {
          this.saida1.checked = false;
          this.saida1.tested = false;
          this.saida1.worked = false;
        } else if (saida === 2) {
          this.saida2.checked = false;
          this.saida2.tested = false;
          this.saida2.worked = false;
        }
      },
    },
  };
  </script>
  
  
  
  
  
  