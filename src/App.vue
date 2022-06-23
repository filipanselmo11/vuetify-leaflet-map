<template>
  <v-app>
    <v-app-bar app  dark>
      <v-toolbar>
        <v-toolbar-title>Vuetify + Vue + Leaflet</v-toolbar-title>
      </v-toolbar>
    </v-app-bar>

    <v-main>
      <mapa-component></mapa-component>
    </v-main>
  </v-app>
</template>

<script>
import MapaComponent from "./components/MapaComponent.vue";
export default {
  name: "App",

  components: { MapaComponent },

  data: () => ({
    //
  }),
};
</script>
