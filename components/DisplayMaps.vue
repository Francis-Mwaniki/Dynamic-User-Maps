<template>
  <div>hello from mapping</div>
</template>

<script>
/*  ['nuxt-supabase', {
    supabaseUrl: 'https://btozlwgodrieiivvilno.supabase.co',
    supabaseKey: 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6ImJ0b3psd2dvZHJpZWlpdnZpbG5vIiwicm9sZSI6ImFub24iLCJpYXQiOjE2NjkzNzQ2NDksImV4cCI6MTk4NDk1MDY0OX0.mCLYF2ZKas2hOfAUapacMUqysLPLgKfz3tRp99MrIYg'
  }] */
import { createClient } from "@supabase/supabase-js";
import { ref } from "vue";
export default {
  data() {
    return {
      locs: null,
    };
  },
  setup() {
    const supabaseUrl = "https://btozlwgodrieiivvilno.supabase.co";
    const supabaseKey =
      "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6ImJ0b3psd2dvZHJpZWlpdnZpbG5vIiwicm9sZSI6ImFub24iLCJpYXQiOjE2NjkzNzQ2NDksImV4cCI6MTk4NDk1MDY0OX0.mCLYF2ZKas2hOfAUapacMUqysLPLgKfz3tRp99MrIYg";
    const supabase = createClient(supabaseUrl, supabaseKey);
    const locs = ref("");
    async function getLocations() {
      const { data, error } = await supabase
        .from("locations")
        .select("*")
        .order("created_at", { descending: true });
      if (error) {
        console.log(error);
      }
      let res = JSON.stringify(data);
      locs.value = data;
      console.table(locs.value);
    }
    getLocations();
    return { getLocations, locs };
  },
};
</script>

<style scoped></style>
