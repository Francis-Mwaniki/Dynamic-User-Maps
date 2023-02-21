<template>
  <div>
    <div class="">
      <div
        class="fixed top-0 left-0 right-0 bottom-0 w-full h-screen z-50 overflow-hidden bg-gray-900 opacity-75 flex flex-col items-center justify-center"
        v-show="!load"
      >
        <h2 class="text-center dark:text-pink-300 text-indigo-100 text-xl font-semibold">
          <img src="../assets/img/ripple.gif" class="bg-slate-900 w-20 h-20" alt="" />
        </h2>
        <p class="sm:w-1/3 w-2/3 text-center text-white text-2xl">
          it's loading hold on.....
        </p>
        <ClientOnly>
          <button
            class="btn-3 ring-1 ring-white hover:bg-slate-200 bg-gray-100 rounded-lg text-black font-bold py-2 px-4 mt-4"
            @click="load = false"
          >
            Rollback
          </button>
        </ClientOnly>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["load"],
};
</script>

<style scoped></style>
