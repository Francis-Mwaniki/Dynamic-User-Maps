<template>
  <main>
    <div
      class="md:justify-end flex md:items-center justify-start items-start text-white gap-5 px-6 md:px-32 py-3 md:py-5 bg-slate-600"
      v-show="load"
    >
      <nuxt-link to="/" class="flex items-center gap-2">
        <span>Home</span>
      </nuxt-link>
      <nuxt-link to="#" class="flex items-center gap-2">
        <span>Refresh map</span>
      </nuxt-link>
      <nuxt-link to="#" class="flex items-center gap-2">
        <span>Logout</span>
      </nuxt-link>
      <button class="px-9 py-3 bg-red-600 rounded hidden">Login</button>
    </div>
    <span class="flex justify-center items-center mx-auto text-lg text-pink-700"
      >If the actual location isn't displayed consider requesting your user to
      Refresh</span
    >
    <div v-if="!load">
      <Loader :load="load" />
    </div>

    <div id="map-wrap" class="" style="height: 100vh" v-else>
      <client-only>
        <l-map :zoom="15" :center="[latitude, longitude]">
          <l-tile-layer url="http://{s}.tile.osm.org/{z}/{x}/{y}.png"></l-tile-layer>
          <l-marker :lat-lng="[latitude, longitude]"></l-marker>
        </l-map>
      </client-only>
    </div>
  </main>
</template>

<script>
import Loader from "./Loader.vue";
import { createClient } from "@supabase/supabase-js";

export default {
  props: ["latitude", "longitude"],
  data() {
    return {
      load: false,
      client: createClient(
        "https://btozlwgodrieiivvilno.supabase.co",
        "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6ImJ0b3psd2dvZHJpZWlpdnZpbG5vIiwicm9sZSI6ImFub24iLCJpYXQiOjE2NjkzNzQ2NDksImV4cCI6MTk4NDk1MDY0OX0.mCLYF2ZKas2hOfAUapacMUqysLPLgKfz3tRp99MrIYg"
      ),
    };
  },
  methods: {
    /*  getLatestLocation() {
      this.client
        .from("locations")
        .select("latitude, longitude")
        .order("created_at", { ascending: false })
        .limit(1)
        .then(({ data }) => {
          const latestLatitude = data[0]?.latitude;
          const latestLongitude = data[0]?.longitude;
          console.log("Latest location:", latestLatitude, latestLongitude);
        })
        .catch((error) => {
          console.error("Error getting latest location:", error);
        });
    }, */
  },
  mounted() {
    setTimeout(() => {
      this.load = true;
    }, 10000);
  },
  components: { Loader },
};
</script>
