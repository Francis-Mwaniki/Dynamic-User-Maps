<template>
  <main>
    <!--
    This component uses @tailwindcss/forms
  
    yarn add @tailwindcss/forms
    npm install @tailwindcss/forms
  
    plugins: [require('@tailwindcss/forms')]
  -->

    <div class="mx-auto max-w-screen-xl px-4 py-16 sm:px-6 lg:px-8">
      <div class="mx-auto max-w-lg">
        <h1 class="text-center text-2xl font-bold text-indigo-600 sm:text-3xl">
          Welcome Back :)
        </h1>
        <h1 class="text-center text-2xl font-bold text-indigo-600 sm:text-3xl">
          Track Your Buddy
        </h1>

        <p class="mx-auto mt-4 max-w-md text-center text-gray-500">
          With Just a single token you can track your Buddy! Right from your comfort Zone!
        </p>
        <!-- success alert  -->
        <div
          class="bg-green-100 border border-green-400 text-green-700 px-4 py-3 rounded relative"
          role="alert"
          v-show="user"
        >
          {{ user }} Logged In!
        </div>
        <!-- warning alert -->
        <div
          class="bg-red-100 border border-red-400 text-red-700 px-4 py-3 rounded relative"
          role="alert"
          v-show="err"
        >
          {{ err }}!
        </div>
        <form
          action=""
          class="mt-6 mb-0 space-y-4 rounded-lg p-8 shadow-2xl"
          @submit.prevent="submit"
        >
          <p class="text-lg font-medium">Sign in to your account</p>

          <div>
            <label for="email" class="text-sm font-medium">Email</label>

            <div class="relative mt-1">
              <input
                type="email"
                v-model="email"
                id="email"
                class="w-full rounded-lg ring p-4 pr-12 text-sm shadow-sm bg-slate-100"
                placeholder="Enter email"
              />

              <span class="absolute inset-y-0 right-4 inline-flex items-center">
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  class="h-5 w-5 text-gray-400"
                  fill="none"
                  viewBox="0 0 24 24"
                  stroke="currentColor"
                >
                  <path
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-width="2"
                    d="M16 12a4 4 0 10-8 0 4 4 0 008 0zm0 0v1.5a2.5 2.5 0 005 0V12a9 9 0 10-9 9m4.5-1.206a8.959 8.959 0 01-4.5 1.207"
                  />
                </svg>
              </span>
            </div>
          </div>

          <div>
            <label for="password" class="text-sm font-medium">Password</label>

            <div class="relative mt-1">
              <input
                type="password"
                v-model="password"
                id="password"
                class="w-full rounded-lg ring p-4 pr-12 text-sm shadow-sm bg-slate-100"
                placeholder="Enter password"
              />

              <span class="absolute inset-y-0 right-4 inline-flex items-center">
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  class="h-5 w-5 text-gray-400"
                  fill="none"
                  viewBox="0 0 24 24"
                  stroke="currentColor"
                >
                  <path
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-width="2"
                    d="M15 12a3 3 0 11-6 0 3 3 0 016 0z"
                  />
                  <path
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-width="2"
                    d="M2.458 12C3.732 7.943 7.523 5 12 5c4.478 0 8.268 2.943 9.542 7-1.274 4.057-5.064 7-9.542 7-4.477 0-8.268-2.943-9.542-7z"
                  />
                </svg>
              </span>
            </div>
          </div>

          <button
            type="submit"
            class="block w-full rounded-lg bg-indigo-600 px-5 py-3 text-sm font-medium text-white"
          >
            Sign in
          </button>

          <p class="text-center text-sm text-gray-500">
            No account?
            <Nuxt-Link to="/" class="underline">Sign up</Nuxt-Link>
          </p>
        </form>
      </div>
    </div>
  </main>
</template>

<script>
import { createClient } from "@supabase/supabase-js";

export default {
  name: "Register",
  data() {
    return {
      email: "",
      user: "",
      password: "",
      warn: "",
      err: "",
    };
  },
  components: {},
  methods: {
    async submit() {
      const supabase = createClient(
        "https://btozlwgodrieiivvilno.supabase.co",
        "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6ImJ0b3psd2dvZHJpZWlpdnZpbG5vIiwicm9sZSI6ImFub24iLCJpYXQiOjE2NjkzNzQ2NDksImV4cCI6MTk4NDk1MDY0OX0.mCLYF2ZKas2hOfAUapacMUqysLPLgKfz3tRp99MrIYg"
      );

      if (this.password.length < 8) {
        alert("Password must be at least 8 characters long");
        return;
      }

      const { data, error } = await supabase.auth.signInWithPassword({
        email: this.email,
        password: this.password,
      });
      if (error) {
        this.err = error.message;
        console.log(error.message);
      } else {
        this.user = data.user.email;
        setTimeout(() => {
          this.$router.push("/Category");
        }, 2000);

        //this.$router.push("/Login");
      }
    },
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Quantico&display=swap");
* {
  font-family: "Quantico", sans-serif;
  transition: all 0.2s ease-in-out;
  scroll-behavior: smooth;
}
</style>
