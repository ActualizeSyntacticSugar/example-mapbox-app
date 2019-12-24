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
      message: "Welcome to Vue.js!",
      places: [
        { lat: -25.363, lng: 131.044, description: "A place in Australia" },
        { lat: -33.8675, lng: 151.207, description: "The main city!" }
      ]
    };
  },
  created: function() {},
  mounted: function() {
    mapboxgl.accessToken = process.env.VUE_APP_MAPBOX_KEY;
    var map = new mapboxgl.Map({
      container: "map", // container id
      style: "mapbox://styles/mapbox/streets-v11", // stylesheet location
      center: [this.places[0].lng, this.places[0].lat], // starting position [lng, lat]
      zoom: 3 // starting zoom
    });
    // WITHOUT A LOOP
    // var popup = new mapboxgl.Popup({ offset: 25 }).setText(this.places[0].description);
    // var marker = new mapboxgl.Marker()
    //   .setLngLat([this.places[0].lng, this.places[0].lat])
    //   .setPopup(popup)
    //   .addTo(map);
    // var popup2 = new mapboxgl.Popup({ offset: 25 }).setText(this.places[1].description);
    // var marker2 = new mapboxgl.Marker()
    //   .setLngLat([this.places[1].lng, this.places[1].lat])
    //   .setPopup(popup2)
    //   .addTo(map);

    // WITH A WHILE LOOP
    // var index = 0;
    // while (index < this.places.length) {
    //   var place = this.places[index];
    //   var popup = new mapboxgl.Popup({ offset: 25 }).setText(place.description);
    //   var marker = new mapboxgl.Marker()
    //     .setLngLat([place.lng, place.lat])
    //     .setPopup(popup)
    //     .addTo(map);
    //   index += 1;
    // }

    // WITH A forEach LOOP
    this.places.forEach(function(place) {
      var popup = new mapboxgl.Popup({ offset: 25 }).setText(place.description);
      var marker = new mapboxgl.Marker()
        .setLngLat([place.lng, place.lat])
        .setPopup(popup)
        .addTo(map);
    });
  },
  methods: {}
};
</script>
