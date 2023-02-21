<template>
  <main>
    <div
      class="md:justify-end flex md:items-center justify-start items-start text-white gap-5 px-6 md:px-32 py-3 md:py-5 bg-slate-600"
      v-show="load"
    >
      <NuxtLink to="/" class="flex items-center gap-2">
        <Icon name="teenyicons:home-solid" class="w-6 h-6" />
        <span>Home</span>
      </NuxtLink>
      <NuxtLink to="/movies" class="flex items-center gap-2">
        <Icon name="bxs:movie-play" class="w-6 h-6" />
        <span>Refresh map</span>
      </NuxtLink>
      <NuxtLink to="/categorySearch" class="flex items-center gap-2">
        <Icon name="teenyicons:search-circle-solid" class="w-6 h-6" />
        <span>Logout</span>
      </NuxtLink>
      <button class="px-9 py-3 bg-red-600 rounded hidden">Login</button>
    </div>
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

export default {
  props: ["latitude", "longitude"],
  data() {
    return {
      load: false,
    };
  },
  mounted() {
    setTimeout(() => {
      this.load = true;
    }, 8000);
  },
  components: { Loader },
};
</script>
