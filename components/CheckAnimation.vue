<template>
    <div v-if="showCheck" class="auto-animation">
      <v-icon class="check-icon" @click="toggleCheck">{{ 'mdi-check-circle' }}</v-icon>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        showCheck: false,
      };
    },
    mounted() {
      // Delay para iniciar a animação após um curto período de tempo
      setTimeout(() => {
        this.showCheck = true;
      }, 700); // Ajuste o tempo conforme necessário
    },
    methods: {
      toggleCheck() {
        this.showCheck = !this.showCheck;
      },
    },
  };
  </script>
  
  <style scoped>
  .auto-animation {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    animation: fadeInUp 1s ease-in-out;
  }
  
  .check-icon {
    font-size: 300px;
    color: green;
    cursor: pointer;
    transition: transform 0.3s;
  }
  
  @keyframes fadeInUp {
    from {
      opacity: 0;
      transform: translateY(20px);
    }
    to {
      opacity: 1;
      transform: translateY(0);
    }
  }
  </style>
  