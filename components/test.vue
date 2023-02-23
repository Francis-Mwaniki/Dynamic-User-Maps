<template>
  <div class="bg-slate-900 min-h-screen">
    <div
      class="md:justify-end flex md:items-center justify-start items-start text-white gap-5 px-6 md:px-32 py-3 md:py-5 bg-slate-900"
      v-show="load"
    >
      <nuxt-link to="/Maps" class="flex items-center gap-2">
        <span>(----).</span>
      </nuxt-link>
      <nuxt-link to="#" class="flex items-center gap-2">
        <span>Login</span>
      </nuxt-link>
      <button class="px-9 py-3 bg-red-600 rounded hidden">Login</button>
    </div>
    <div
      class="flex flex-col justify-center items-center mx-auto my-2 rounded bg-slate-900 text-white"
      v-show="load"
    >
      <!-- display my name -->
      <div>
        <form
          action=""
          class="flex mx-auto justify-center items-center ring-1 ring-white rounded p-1"
          @submit.prevent="submit"
          v-show="signing"
        >
          <label for="name" class="px-2 border-r border-white">Your name</label>
          <input
            type="text"
            name="name"
            id="name"
            v-model="name"
            class="bg-slate-900 text-white border-none outline-none focus:underline"
          />
          <button
            type="submit"
            class="bg-blue-700 text-white border-none outline-none focus:underline px-3 py-1 border-l border-white"
          >
            Submit
          </button>
        </form>
      </div>
      <span class="text-lg text-white">Hi {{ firstname }}!</span>

      <currentPlace :locs="locs" />
    </div>
    <div v-if="!load">
      <Loader :load="load" />
    </div>
  </div>
</template>

<script>
//import L from "leaflet";
import { createClient } from "@supabase/supabase-js";
import currentPlace from "./currentPlace.vue";

export default {
  data() {
    return {
      client: createClient(
        "https://btozlwgodrieiivvilno.supabase.co",
        "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6ImJ0b3psd2dvZHJpZWlpdnZpbG5vIiwicm9sZSI6ImFub24iLCJpYXQiOjE2NjkzNzQ2NDksImV4cCI6MTk4NDk1MDY0OX0.mCLYF2ZKas2hOfAUapacMUqysLPLgKfz3tRp99MrIYg"
      ),
      latitude: null,
      name: "",
      longitude: null,
      signing: true,
      load: false,
      firstname: "",
      locs: [],
    };
  },
  components: {
    currentPlace,
  },

  methods: {
    /*   setupMap() {
      const map = L.map(this.$refs.map).setView([51.505, -0.09], 13);

      L.tileLayer("https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png", {
        attribution:
          'Map data © <a href="https://openstreetmap.org">OpenStreetMap</a> contributors',
        maxZoom: 18,
      }).addTo(map);

      this.map = map;
    },
 */
    /*   addMarker(latlng) {
      const marker = L.marker(latlng).addTo(this.map);
      this.markers.push(marker);
    },

    removeMarkers() {
      this.markers.forEach((marker) => this.map.removeLayer(marker));
      this.markers = [];
    }, */

    /*    addLocationToSupabase(latlng) {
      this.client
        .from("locations")
        .insert([{ location: latlng }])
        .then(() => {
          console.log("Location added to Supabase:", latlng);
        })
        .catch((error) => {
          console.error("Error adding location to Supabase:", error);
        });
    }, */
    submit() {
      this.firstname = this.name;
      setTimeout(() => {
        this.signing = false;
      }, 1000);
    },

    async listenForLocationChanges() {
      /* subscribe to new locations thro channel changes from supabase */
      const subs = this.client
        .channel("locations")
        .on(
          "postgres_changes",
          { event: "INSERT", schema: "public", table: "locations" },
          (payload) => {
            console.log("Change received!", payload);
          }
        )
        .subscribe();
    },

    getCurrentPosition() {
      navigator.geolocation.getCurrentPosition(
        (position) => {
          const { latitude, longitude } = position.coords;
          fetch(
            `https://nominatim.openstreetmap.org/reverse?format=json&lat=${latitude}&lon=${longitude}`
          )
            .then((response) => {
              return response.json();
            })
            .then((data) => {
              console.log(data);
              this.locs.push({
                location: data.display_name,
                city: data.address.city,
                latitude: latitude,
                longitude: longitude,
                accuracy: position.coords.accuracy,
              });
              this.load = true;
            });
          console.log(latitude, longitude);
        },
        (error) => {
          console.error("Error getting current position:", error);
        }
      );
    },
    watchCurrentPosition() {
      const options = {
        enableHighAccuracy: true,
        timeout: 5000,
        maximumAge: 0,
      };
      const success = (pos) => {
        const crd = pos.coords;
        /// console.log("Your current position is:");
        // console.log(`Latitude : ${crd.latitude}`);
        //  console.log(`Longitude: ${crd.longitude}`);
        // console.log(`More or less ${crd.accuracy} meters.`);
        //console.log(crd);
        this.latitude = crd.latitude;
        this.longitude = crd.longitude;
        /* insert new locations(latitude and longitude) to supabase */
        this.client
          .from("locations")
          .insert([{ latitude: this.latitude, longitude: this.longitude }])
          .then(() => {
            console.log("Location added to Supabase:", this.latitude);
          })
          .catch((error) => {
            console.error("Error adding location to Supabase:", error);
          });
      };
      const error = (err) => {
        console.warn(`ERROR(${err.code}): ${err.message}`);
      };
      navigator.geolocation.watchPosition(success, error, options);
    },
  },

  mounted() {
    //this.setupMap();
    //   this.getCurrentPosition();
    this.watchCurrentPosition();
    this.getCurrentPosition();
    setTimeout(() => {
      this.load = true;
    }, 5000);
  },
};
</script>

<style></style>
