<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <div id="map"></div>
  </div>
</template>

<style>
#map {
  height: 300px;
}
</style>

<script>
/* global mapboxgl, mapboxSdk */

export default {
  data: function() {
    return {
      message: "Welcome to Vue.js!",
      places: [
        { address: "222 Merchandise Mart Plz, Chicago", description: "Merchandise Mart" },
        { address: "215 W Ohio, Chicago", description: "Actualize" }
      ]
    };
  },
  created: function() {},
  mounted: function() {
    mapboxgl.accessToken = process.env.VUE_APP_MAPBOX_KEY;
    var mapboxClient = mapboxSdk({ accessToken: mapboxgl.accessToken });

    var map = new mapboxgl.Map({
      container: "map",
      style: "mapbox://styles/mapbox/streets-v11",
      center: [-87.62, 41.88],
      zoom: 12
    });

    this.places.forEach(function(place) {
      mapboxClient.geocoding
        .forwardGeocode({
          query: place.address,
          autocomplete: false,
          limit: 1
        })
        .send()
        .then(function(response) {
          if (response && response.body && response.body.features && response.body.features.length) {
            var feature = response.body.features[0];

            new mapboxgl.Marker().setLngLat(feature.center).addTo(map);
          }
        });
    });
  },
  methods: {}
};
</script>
