<template>
  <div class="container">
    <div id="googleMap"></div>
    <div id="btn-sec">
      <button class="btn-green btn-big">Start</button>
      <button class="btn-green btn-big">Stop</button>
    </div>
  </div>
</template>

<script>
import { testActions } from "../../actions/gpsTracking.action";

export default {
  name: "TestComp",
  components: {},
  data() {
    return { data: {} };
  },
  methods: {
    // getData() {
    //   testActions
    //     .getData()
    //     .then(this.successHandle)
    //     .catch(this.errorHandle);
    // },

    myMapData(data) {
      console.log("data---------", data);
      let propLatLng = { lat: data.lat, lng: data.lng };
      let getElementById = document.getElementById("googleMap");
      let propMap = { zoom: 8, center: propLatLng };
      let map = new google.maps.Map(getElementById, propMap);
      let propMarker = { position: propLatLng, map: map, title: "Marker...." };
      var marker = new google.maps.Marker(propMarker);
    },
    getMapData() {
      testActions
        .getMapData()
        .then(this.successHandle)
        .catch(this.errorHandle);
    },
    successHandle(data) {
      this.myMapData(data);
    },
    errorHandle(error) {}
  },
  mounted() {
    //this.getData();
    this.getMapData();
  }
};
</script>