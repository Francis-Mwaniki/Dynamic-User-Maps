<template>
  <div>
    <Test />
  </div>
</template>

<script>
//import DisplayMaps from "../components/DisplayMaps.vue";
import Test from "../components/test.vue";

export default {
  components: { Test },
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
