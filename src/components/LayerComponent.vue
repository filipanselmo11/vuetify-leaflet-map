<template>
  <v-container fluid>
    <v-checkbox
      v-for="layer in layers"
      :key="layer.id"
      :label="layer.name"
      v-model="layer.active"
      @change="layerChanged(layer.id, layer.active)"
    >
    </v-checkbox>
  </v-container>
</template>

<script>
export default {
  name: "LayerComponent",
  props: ["map"],
  data() {
    return {
      layers: [
        {
          id: 0,
          name: "Escolas da UEA",
          active: false,
          features: [
            {
              id: 0,
              name: "Escola Superior de Tecnologia",
              type: "circle",
              coords: [-3.091657310963936, -60.0172456309875],
            },
            {
              id: 1,
              name: "Escola Superior de Ciências da Saúde",
              type: "circle",
              coords: [-3.1190563612562725, -60.00612814448035],
            },
            {
              id: 2,
              name: "Escola Normal Superior",
              type: "circle",
              coords: [-3.0924640070994904, -60.023583402151715],
            },
            {
              id: 3,
              name: "Escola Superior de Artes e Turismo",
              type: "circle",
              coords: [38.617972, -90.2756436],
            },
            {
              id: 4,
              name: "Escola Superior de Ciências Sociais",
              type: "circle",
              coords: [-3.125673178859916, -60.02206618865858],
            },
          ],
        },
        {
          id: 1,
          name: "Locais da Cidade",
          active: false,
          features: [
            {
              id: 0,
              name: "Cidade de Manaus",
              type: "polygon",
              coords: [
                [-3.1277514745460064, -60.02597148484211],
                [-3.1220843595646004, -60.03373916214339],
                [-3.1106000554217537, -60.03987605650147],
                [-3.1007647523982915, -60.024485481452274],
                [-3.0981275424590042, -60.017927454310424],
                [-3.0876423386412144, -60.005653480895944],
              ],
            },
          ],
        },
      ],
      checkbox1: true,
      checkbox2: false,
    };
  },
  mounted() {
    this.initLayers();
  },
  methods: {
    initLayers() {
      this.layers.forEach((layer) => {
        const circleFeatures = layer.features.filter(
          (feature) => feature.type === "circle"
        );
        console.log("CIRCLE FEATURES ", circleFeatures);
        const polygonFeatures = layer.features.filter(
          (feature) => feature.type === "polygon"
        );

        console.log("POLYGON FEATURES ", polygonFeatures);

        circleFeatures.forEach((feature) => {
          feature.leafletObject = L.circle(feature.coords).bindPopup(feature.name);
        });

        polygonFeatures.forEach((feature) => {
          feature.leafletObject = L.polygon(feature.coords).bindPopup(feature.name);
        });
      });
    },
    layerChanged(layerId, active) {
      const layer = this.layers.find((layer) => layer.id === layerId);
      layer.features.forEach((feature) => {
        if (active) {
          feature.leafletObject.addTo(this.map);
        } else {
          feature.leafletObject.removeFrom(this.map);
        }
      });
    },
  },
};
</script>

<style></style>
