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
// import "leaflet-ruler/src/leaflet-ruler.css";
// import "leaflet-ruler";
// import "leaflet-simple-map-screenshoter";

// import "leaflet-velocity/dist/leaflet-velocity.css";
// import "leaflet-velocity";

delete L.Icon.Default.prototype._getIconUrl;
L.Icon.Default.mergeOptions({
  iconRetinaUrl: require("leaflet/dist/images/marker-icon-2x.png"),
  iconUrl: require("leaflet/dist/images/marker-icon.png"),
  shadowUrl: require("leaflet/dist/images/marker-shadow.png"),
});

var drawnItems = new L.FeatureGroup();
var drawControl = new L.Control.Draw({
  edit: {
    featureGroup: drawnItems,
  },
});

export default {
  name: "MapDraw",
  data: () => ({
    map: {},
    layerControl: null,
    editableLayers: null,
    // drawControl: null,
    circles: null,
    polygon: null,
    refreshing: null,
    simpleMapScreenshoter: null,
    imageAlertScreenshot: null,
  }),
  //   created(){
  //     this.refreshLayers();
  //   },
  mounted() {
    // var _this = this;
    //Inicializando mapa
    this.initMap();
    //inicializando outros layers
    // this.initLayers();
    //carregar carregar camadas editáveis ​​para desenhos
    // var editable = this.editableLayers;
    //escute faça desenhos e salve então na camada editável
    // this.map.on(L.Draw.Event.CREATED, function (e) {
    //   var type = e.layerType,
    //     layer = e.layer;
    // });
  },
  methods: {
    initMap() {
      this.map = L.map("map", { drawControl: true }).setView(
        [-0.13043324879318963, -67.08780940856025],
        13
      );
      L.tileLayer("http://{s}.tile.osm.org/{z}/{x}/{y}.png", {
        attribution:
          '&copy; <a href="http://osm.org/copyright">OpenStreetMap</a> contributors',
      }).addTo(this.map);
      this.map.addLayer(drawnItems);
      this.map.addControl(drawControl);
    },
  },
};
</script>

<style>
#map {
  height: 600px;
}
</style>
