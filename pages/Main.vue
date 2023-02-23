<template>
  <div>
    <div>
      <div class="">
        <div
          class="fixed top-0 left-0 right-0 bottom-0 w-full h-screen z-50 overflow-hidden bg-gray-900 opacity-75 flex flex-col items-center justify-center"
          v-show="loading"
        >
          <h2
            class="text-center dark:text-pink-300 text-indigo-100 text-xl font-semibold"
          >
            <img src="../assets/img/ripple.gif" class="bg-slate-900 w-20 h-20" alt="" />
          </h2>
          <p class="sm:w-1/3 w-2/3 text-center text-white text-2xl">
            it's loading hold on.....
          </p>
        </div>
      </div>
    </div>
    <Test />
  </div>
</template>

<script>
//import DisplayMaps from "../components/DisplayMaps.vue";
//import Loadinger from "../components/Loadinger.vue";
import Test from "../components/test.vue";

export default {
  components: { Test },
  data() {
    return {
      loading: true,
    };
  },
  mounted() {
    setTimeout(() => {
      this.loading = false;
    }, 1000);
  },
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Quantico&display=swap");
* {
  font-family: "Quantico", sans-serif;
  transition: all 0.2s ease-in-out;
  scroll-behavior: smooth;
}
</style>
