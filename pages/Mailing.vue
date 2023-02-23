<template>
  <div>
    <SendMail />
  </div>
</template>

<script>
import SendMail from "../components/SendMail.vue";

export default {
  components: { SendMail },
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
