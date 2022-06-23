<template>
  <v-container>
    <v-card>
      <div id="map"></div>
    </v-card>
  </v-container>
</template>

<script>
import L from "leaflet";
import "leaflet/dist/leaflet.css";

// var CustomIcon = L.Icon.extend({
//   options: {
//     iconSize: [38, 95],
//     iconAnchor: [50, 64],
//     popupAnchor: [-3, -76],
//   },
// });

// var icone = CustomIcon({iconUrl: '/assets/location-icon.png'});

var icone = L.icon({
  // iconUrl: 'map-marker-radius',
  iconUrl: '/assets/location-icon.png',
  iconSize: [38, 93],
  iconAnchor: [22, 94],
});

var manaus = L.marker([-3.11866, -60.0212], { icon: icone }).bindPopup("Manaus"),
  belem = L.marker([-6.74261, -35.5166], { icon: icone }).bindPopup("Belem"),
  brasilia = L.marker([-15.7795, -47.9297], { icon: icone }).bindPopup("Brasilia"),
  natal = L.marker([-5.79357, -35.1986], { icon: icone }).bindPopup("Natal"),
  sgc = L.marker([-0.13043324879318963, -67.08780940856025], { icon: icone }).bindPopup(
    "São Gabriel da Cachoeira"
  );

var cidades = L.layerGroup([manaus, belem, brasilia, natal, sgc]);

var osm = L.tileLayer("https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png", {
  maxZoom: 19,
  attribution: "© OpenStreetMap",
});

var praiaPipa = L.marker([-6.226510091221283, -35.04496734216885], {
    icon: icone,
  }).bindPopup("Praia de Pipa"),
  teatroAmazonas = L.marker([-3.1300424026467826, -60.02342493098717], {
    icon: icone,
  }).bindPopup("Teatro Amazonas");

var locais = L.layerGroup([praiaPipa, teatroAmazonas]);

var satelite = L.tileLayer("http://{s}.google.com/vt/lyrs=s&x={x}&y={y}&z={z}", {
  maxZoom: 20,
  subdomains: ["mt0", "mt1", "mt2", "mt3"],
});

var ruas = L.tileLayer("https://tileserver.memomaps.de/tilegen/{z}/{x}/{y}.png", {
  maxZoom: 18,
  attribution:
    'Map <a href="https://memomaps.de/">memomaps.de</a> <a href="http://creativecommons.org/licenses/by-sa/2.0/">CC-BY-SA</a>, map data &copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors',
});

var baseMaps = {
  OpenStreetMap: osm,
  "Map Ruas": ruas,
  // "<span style='color: gray'>GrayScale</span>": grayscale
};

var overlayMaps = {
  Cidades: cidades,
};

export default {
  name: "Mapa1",
  data() {
    return {
      map: undefined,
      layerControl: undefined,
    };
  },
  mounted() {
    this.initMap();
  },
  methods: {
    initMap() {
      this.map = L.map("map", {
        center: [-8.359639010938677, -55.40120007970321],
        zoom: 10,
        layers: [osm, cidades],
      });
      this.layerControl = L.control.layers(baseMaps, overlayMaps).addTo(this.map);
      this.layerControl.addBaseLayer(satelite, "Satelite");
      this.layerControl.addOverlay(locais, "Locais");
    },
  },
};
</script>

<style>
#map {
  height: 600px;
}
</style>
