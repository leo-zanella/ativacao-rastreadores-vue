<template>
  <v-container>
    <div id="camera"></div>
    <v-card-text>{{ codigo }}</v-card-text>
  </v-container>
</template>

<script>
import Quagga from 'quagga';
// import adapter from 'webrtc-adapter';


export default {
  data() {
    return {
      codigo: null,
      codigoCorrigido: null,
    };
  },
  mounted() {
    Quagga.init(
      {
        inputStream: {
          name: 'Live',
          type: 'LiveStream',
          target: document.querySelector('#camera'),
        },
        decoder: {
          readers: ['code_128_reader'],
        },
      },
      (err) => {
        if (err) {
          console.error(err);
          return;
        }
        Quagga.start();
      }
    );

    Quagga.onDetected((data) => {
      this.codigo = data.codeResult.code.substring(2,12);
    });
  },
  methods: {
    retirarDigitos(code) {
      return code.substring(2, 12);
    },
  },
};
</script>

<style>
</style>
