<template>
  <v-container>
    <v-card>
      <div id="map"></div>
    </v-card>
  </v-container>
</template>

<script>
import "leaflet/dist/leaflet.css";
import L from "leaflet";
import "leaflet-draw/dist/leaflet.draw.css";
import "leaflet-draw";

delete L.Icon.Default.prototype._getIconUrl;
L.Icon.Default.mergeOptions({
  iconRetinaUrl: require("leaflet/dist/images/marker-icon-2x.png"),
  iconUrl: require("leaflet/dist/images/marker-icon.png"),
  shadowUrl: require("leaflet/dist/images/marker-shadow.png"),
});

// var toolbar = L.Toolbar();

//disabling a toolbar
var drawControl = new L.Control.Draw({
  draw: false,
//   edit: {
//     featureGroup: editableLayers,
//   },
});

export default {
  name: "MapDraw",
  data: () => ({
    map: undefined,
  }),
  mounted() {
    this.initMap();
  },
  methods: {
    initMap() {
      this.map = L.map("map", {drawControl: drawControl}).setView(
        [-8.359639010938677, -55.40120007970321],
        5
      );
      L.tileLayer("http://{s}.tile.osm.org/{z}/{x}/{y}.png", {
        attribution:
          '&copy; <a href="http://osm.org/copyright">OpenStreetMap</a> contributors',
      }).addTo(this.map);
    },
  },
};
</script>

<style>
#map {
  height: 600px;
}
</style>
