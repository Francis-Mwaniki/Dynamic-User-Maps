<template>
  <div>
    <GeoMap :latitude="latitude" :longitude="longitude" />
  </div>
</template>

<script>
import GeoMap from "./Geo-map.vue";
import { createClient } from "@supabase/supabase-js";

export default {
  data() {
    return {
      client: createClient(
        "https://btozlwgodrieiivvilno.supabase.co",
        "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6ImJ0b3psd2dvZHJpZWlpdnZpbG5vIiwicm9sZSI6ImFub24iLCJpYXQiOjE2NjkzNzQ2NDksImV4cCI6MTk4NDk1MDY0OX0.mCLYF2ZKas2hOfAUapacMUqysLPLgKfz3tRp99MrIYg"
      ),
      latitude: null,
      longitude: null,
    };
  },
  mounted() {
    /*   this.getLocation(); */
    this.getLatestLocation();
  },
  created() {},

  methods: {
    getLatestLocation() {
      this.client
        .from("locations")
        .select("latitude, longitude")
        .order("created_at", { ascending: false })
        .limit(1)
        .then(({ data }) => {
          const latestLatitude = data[0]?.latitude;
          const latestLongitude = data[0]?.longitude;
          this.latitude = latestLatitude ? latestLatitude : -1.23322;
          this.longitude = latestLongitude ? latestLongitude : 36.88333;
          console.log("Latest location:", latestLatitude, latestLongitude);
        })
        .catch((error) => {
          console.error("Error getting latest location:", error);
        });
    },
    // use watchCurentPosition() in the mounted() hook
    // to watch the user's position
    /*   watchCurrentPosition() {
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
      };
      const error = (err) => {
        console.warn(`ERROR(${err.code}): ${err.message}`);
      };
      navigator.geolocation.watchPosition(success, error, options);
    }, */
    /* use latitude and longitude to map using google map reverse geocoding */
  },

  components: { GeoMap },
};
</script>
