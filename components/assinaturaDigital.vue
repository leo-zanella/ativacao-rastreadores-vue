<template>
    <v-container>
      <v-row>
        <v-col cols="12">
          <v-card-subtitle class="d-flex subtitle-2 justify-center align-center titulo">Assinatura do responsável</v-card-subtitle>
          <div class="signature-container">
            <canvas ref="canvas" class="canvas"></canvas>
          </div>
        </v-col>
      </v-row>
      <v-row>
        <v-col cols="12" class="d-flex justify-center align-center">
          <v-btn color="red" small dark  class="d-flex justify-center align-center mb-5 mt-0" @click="clearSignature">Limpar Assinatura</v-btn>
        </v-col>
      </v-row>
    </v-container>
</template>

<script>
import SignaturePad from 'signature_pad';

export default {
  mounted() {
    this.initializeSignaturePad();
  },
  methods: {
    initializeSignaturePad() {
      const canvas = this.$refs.canvas;
      const options = {
        backgroundColor: 'rgb(255, 255, 255)', // Cor de fundo do canvas
      };

      this.signaturePad = new SignaturePad(canvas, options);
    },
    clearSignature() {
      this.signaturePad.clear();
    },
  },
};
</script>

<style>
.titulo{
  user-select: none;
}

.signature-container {
  display: flex;
  justify-content: center;
}

.canvas {
  user-select: none;
  border: solid 2px black;
  border-radius: 5px;
  background-color: rgb(255, 255, 255);
  background-origin: border-box;
  background-clip: content-box, border-box;
}
</style>
