<template>
  <v-app>
    <v-app-bar app dark>
      <v-toolbar>
        <v-toolbar-title>Vuetify + Vue + Leaflet</v-toolbar-title>
      </v-toolbar>
    </v-app-bar>

    <v-main>
      <map-draw></map-draw>
      <!-- <mapa-component></mapa-component> -->
    </v-main>
  </v-app>
</template>

<script>
import MapDraw from "./components/MapDraw.vue";

// import MapaComponent from "./components/MapaComponent.vue";
export default {
  name: "App",

  components: { MapDraw },

  data: () => ({
    //
  }),
};
</script>
