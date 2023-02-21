<template>
  <div>
    <GeoMap :latitude="latitude" :longitude="longitude" />
  </div>
</template>

<script>
import GeoMap from "./Geo-map.vue";

export default {
  data() {
    return {
      latitude: null,
      longitude: null,
    };
  },
  mounted() {
    /*   this.getLocation(); */
    this.watchCurrentPosition();
  },
  created() {},

  methods: {
    /* async getLocation() {
          try {
            const position = await new Promise((resolve, reject) => {
              navigator.geolocation.getCurrentPosition(resolve, reject);
            });
            console.log(position);
            const { latitude, longitude } = position.coords;
            const url = `http://localhost:3000/location?latitude=${latitude}&longitude=${longitude}`;
            const response = await fetch(url);
            const data = await response.json();
            this.latitude = data.latitude;
            this.longitude = data.longitude;
          } catch (error) {
            console.error(error);
          }
        }, */
    // use watchCurentPosition() in the mounted() hook
    // to watch the user's position
    watchCurrentPosition() {
      const options = {
        enableHighAccuracy: true,
        timeout: 5000,
        maximumAge: 0,
      };
      const success = (pos) => {
        const crd = pos.coords;
        console.log("Your current position is:");
        console.log(`Latitude : ${crd.latitude}`);
        console.log(`Longitude: ${crd.longitude}`);
        console.log(`More or less ${crd.accuracy} meters.`);
        console.log(crd);
        this.latitude = crd.latitude;
        this.longitude = crd.longitude;
      };
      const error = (err) => {
        console.warn(`ERROR(${err.code}): ${err.message}`);
      };
      navigator.geolocation.watchPosition(success, error, options);
    },
    /* use latitude and longitude to map using google map reverse geocoding */
  },
  components: { GeoMap },
};
</script>
