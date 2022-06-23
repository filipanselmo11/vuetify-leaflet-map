<template>
  <v-app>
    <v-app-bar app dark>
      <v-toolbar>
        <v-toolbar-title>Vuetify + Vue + Leaflet</v-toolbar-title>
      </v-toolbar>
    </v-app-bar>

    <v-main>
      <mapa-1></mapa-1>
      <!-- <mapa-component></mapa-component> -->
    </v-main>
  </v-app>
</template>

<script>
import Mapa1 from "./components/Mapa1.vue";
// import MapaComponent from "./components/MapaComponent.vue";
export default {
  name: "App",

  components: { Mapa1 },

  data: () => ({
    //
  }),
};
</script>
