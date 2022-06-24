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

var cloudmadeUrl = 'http://{s}.tile.cloudmade.com/BC9A493B41014CAABB98F0471D759707/997/256/{z}/{x}/{y}.png';
var cloudmade = new L.TileLayer(cloudmadeUrl, {maxZoom: 18});

var editableLayers = new L.FeatureGroup();

var MyCustomMarker = L.Icon.extend({
    options:{
        shadowUrl: null,
        iconAnchor: new L.Point(12, 12),
        iconSize: new L.Point(24, 24),
        iconUrl: 'https://cdn-icons-png.flaticon.com/512/149/149059.png'
    }
});

var options = {
        position: 'topright',
        draw: {
            polyline: {
                shapeOptions: {
                    color: '#f357a1',
                    weight: 10
                }
            },
            polygon: {
                allowIntersection: false, // Restricts shapes to simple polygons
                drawError: {
                    color: '#e1e100', // Color the shape will turn when intersects
                    message: 'Você não pode desenhar isso' // Message that will show when intersect
                },
                shapeOptions: {
                    color: '#bada55'
                }
            },
            circle: false, // Turns off this drawing tool
            rectangle: {
                shapeOptions: {
                    clickable: false
                }
            },
            marker: {
                icon: new MyCustomMarker()
            }
        },
        edit: {
            featureGroup: editableLayers, //REQUIRED!!
            remove: false
        }
    };

var drawControl = new L.Control.Draw(options);



export default {
  name: "MapDraw",
  data: () => ({
    map: undefined,
    tileLayer: undefined,
  }),
  mounted() {
    this.initMap();
  },
  methods: {
    initMap() {
        this.map = new L.map('map', {layers: [cloudmade], center: new L.LatLng(-0.13043324879318963, -67.08780940856025), zoom: 15});
        this.map.addLayer(editableLayers);
        this.map.addControl(drawControl);
        this.map.on(L.Draw.Event.CREATED, function(e) {
            var type = e.layerType;
            var layer = e.layer;

            if(type === 'marker'){
                layer.bindPopup('Um Popup');
            }
            editableLayers.addLayer(layer);
        })
    //   (this.map = L.map("map")).setView([-0.13043324879318963, -67.08780940856025], 12);
    //   this.tileLayer = L.tileLayer(
    //     cloudmadeUrl,
    //     {
    //       maxZoom: 18,
    //       attribution:'&copy; <a href="http://www.openstreetmap.org/copyright">OpenStreetMap</a>, &copy; <a href="https://carto.com/attribution">CARTO</a>',
    //     }
    //   );
    //   this.tileLayer.addTo(this.map);
    },
  },
};
</script>

<style>
#map {
  height: 600px;
}
</style>
