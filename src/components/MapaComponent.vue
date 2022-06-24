<template>
  <v-container>
    <div id="sidebar">
        <ul></ul>
    </div>
    <div id="map"></div>
    <br/>
    <layer-component :map="map"></layer-component>
  </v-container>
</template>

<script>
import L from "leaflet";
import "leaflet/dist/leaflet.css";
// import 'sidebar-v2/css'; 
import LayerComponent from './LayerComponent.vue';
export default {
  components: { LayerComponent },
  name: "MapaComponent",
  data() {
    return {
      map: null,
      sidebar: null,
      tileLayer: null,
    };
  },
  mounted() {
    this.initMap();
  },
  methods: {
    initMap() {
      this.map = L.map("map").setView([-3.10719, -60.0261], 12);
      this.tileLayer = L.tileLayer(
        "https://cartodb-basemaps-{s}.global.ssl.fastly.net/rastertiles/voyager/{z}/{x}/{y}.png",
        {
          maxZoom: 18,
          attribution:
            '&copy; <a href="http://www.openstreetmap.org/copyright">OpenStreetMap</a>, &copy; <a href="https://carto.com/attribution">CARTO</a>',
        }
      );
      this.tileLayer.addTo(this.map);
      // this.sidebar = L.control.sidebar('sidebar').addTo(this.map);
    },
  },
};
</script>

<style>
#map {
  height: 600px;
}
</style>
