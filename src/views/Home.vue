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
/* global mapboxgl */

export default {
  data: function() {
    return {
      message: "Welcome to Vue.js!"
    };
  },
  created: function() {},
  mounted: function() {
    mapboxgl.accessToken = process.env.VUE_APP_MAPBOX_KEY;
    var map = new mapboxgl.Map({
      container: "map", // container id
      style: "mapbox://styles/mapbox/streets-v11", // stylesheet location
      center: [-87.6, 41.8], // starting position [lng, lat]
      zoom: 5 // starting zoom
    });
    var popup = new mapboxgl.Popup({ offset: 25 }).setText("Construction on the Washington Monument began in 1848.");
    var marker = new mapboxgl.Marker()
      .setLngLat([-87.6, 41.8])
      .setPopup(popup)
      .addTo(map);
  },
  methods: {}
};
</script>
