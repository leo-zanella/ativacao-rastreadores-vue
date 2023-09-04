<template>
  <container>
    <div>
      <v-card-title class="d-flex align-center justify-center mb-5">Instalação Concluída!</v-card-title>
      <check-animation></check-animation>
    </div>
  </container>
</template>

<script>
import CheckAnimation from '~/components/CheckAnimation.vue'

export default {
  components: {
    CheckAnimation,
  },
}
</script>
