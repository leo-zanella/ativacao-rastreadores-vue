<template>
  <v-app class="app" id="inspire">

    <v-navigation-drawer
      v-model="drawer"
      app
    >
      <v-card
        class="pt-5 text-center rounded-0"
        color="grey darken-3"
        dark
      >
        <v-avatar size="100" color="white">
          <img src="../assets/Wagner.jpg"/>
        </v-avatar>
        <v-list-item>
          <v-list-item-content>
            <v-list-item-title class="text-h6">
              Wagner
            </v-list-item-title>
            <v-list-item-subtitle class="mt-7">
              Menu
            </v-list-item-subtitle>
          </v-list-item-content>
        </v-list-item>
      </v-card>

      <v-divider></v-divider>

      <v-list dense nav>
        <v-list-item
          v-for="item in items"
          :key="item.title"
          link
          @click="redirectToLink(item)"
        >
          <v-list-item-icon>
            <v-icon :color="item.iconColor">{{ item.icon }}</v-icon>
          </v-list-item-icon>
          <v-list-item-content>
            <v-list-item-title>{{ item.title }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar app prominent elevation="0" color="grey lighten-2">
      <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>

      <div class="tamanhototal d-flex justify-center align-center flex-column">
        <v-img
          class="justify-center align-center mt-5"
          contain
          max-height="56"
          max-width="300"
          :src="require('../assets/logo-rotaexata.svg')"/>
        <v-card-subtitle>Instalador</v-card-subtitle>
      </div>
    </v-app-bar>
    <v-main style="background-color: white;">
      <v-container>
        <Nuxt />
      </v-container>
    </v-main>
  </v-app>
</template>


<script>

export default {
  data: () => ({
    drawer: null,
    items: [
      { title: 'Visitas Agendadas', icon: 'mdi-calendar-month', to: '/' },
      { title: 'Serviços na Garantia', icon: 'mdi-shield-check', to: '/garantia' },
      { title: 'Chamar no WhatsApp', icon: 'mdi-whatsapp', to: 'https://wa.me/5547992862017', iconColor: 'green' },
    ],
  }),

  methods: {

    redirectToLink(item) {
      if (item === this.items[2]) {
        window.open(item.to, '_blank')
      } else {
        this.$router.push(item.to);
      }
    },
  },
};
</script>

<style>
.app{
  user-select: none;
  background-color: white;
}

.tamanhototal {
  flex-grow: 1;
  margin-right: 24px;
}
</style>
