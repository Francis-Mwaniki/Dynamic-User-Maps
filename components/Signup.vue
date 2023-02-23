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
          Start Tracking your Buddy!
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
          {{ user }} created!
        </div>
        <div
          class="bg-green-100 border border-green-400 text-green-700 px-4 py-3 rounded relative"
          role="alert"
          v-show="user"
        >
          Please verify Email to procede!
        </div>
        <!-- warning alert -->
        <div
          class="bg-red-100 border border-red-400 text-red-700 px-4 py-3 rounded relative"
          role="alert"
          v-if="err"
        >
          {{ err }}!
        </div>
        <form
          action=""
          class="mt-6 mb-0 space-y-4 rounded-lg p-8 shadow-2xl"
          @submit.prevent="register"
        >
          <p class="text-lg font-medium">Sign Up to your account</p>

          <div>
            <label for="email" class="text-sm font-medium">Email</label>

            <div class="relative mt-1">
              <input
                type="email"
                id="email"
                v-model="email"
                class="w-full rounded-lg ring bg-slate-100 p-4 pr-12 text-sm shadow-sm"
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
                id="password"
                v-model="password"
                class="w-full rounded-lg ring bg-slate-100 p-4 pr-12 text-sm shadow-sm"
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

          <div>
            <label for="confirm-password" class="text-sm font-medium"
              >Confirm Password</label
            >

            <div class="relative mt-1">
              <input
                type="password"
                id="confirm-password"
                class="w-full rounded-lg ring bg-slate-100 p-4 pr-12 text-sm shadow-sm"
                v-model="confirm_password"
                placeholder="Confirm password"
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
            class="block w-full rounded-lg px-5 py-3 text-sm font-medium text-white"
            :class="loading ? 'bg-gray-500 cursor-not-allowed' : 'bg-indigo-600'"
            :disabled="loading"
          >
            {{ loading ? "Loading..." : "Sign Up" }}
          </button>

          <p class="text-center text-sm text-gray-500">
            Already have an account?
            <NuxtLink to="/Login" class="underline">Sign In</NuxtLink>
          </p>
        </form>
        <div class="flex justify-center items-center text-black">
          <span class="text-lg text-black">Made with ❤️ by Francis_pro</span>
        </div>
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
      loading: false,
      password: "",
      confirm_password: "",
      err: "",
    };
  },
  components: {},
  methods: {
    async register() {
      const supabase = createClient(
        "https://btozlwgodrieiivvilno.supabase.co",
        "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6ImJ0b3psd2dvZHJpZWlpdnZpbG5vIiwicm9sZSI6ImFub24iLCJpYXQiOjE2NjkzNzQ2NDksImV4cCI6MTk4NDk1MDY0OX0.mCLYF2ZKas2hOfAUapacMUqysLPLgKfz3tRp99MrIYg"
      );
      if (this.email.length < 1) {
        this.err = "Email is required";
        return;
      }

      if (this.password.length < 8) {
        this.err = "Password must be at least 8 characters";
        return;
      }
      if (this.password !== this.confirm_password) {
        console.log(this.password, this.confirm_password);
        this.err = "Passwords do not match";
        return;
      }
      /* get user from supabase and check if email exists */
      const main_user = await supabase.auth.getUser();
      /* check if email of the texists  */

      if (!this.email.includes("@")) {
        this.err = "Email is invalid";
        return;
      }
      this.loading = true;
      const { user, data, error } = await supabase.auth.signUp({
        email: this.email,
        password: this.password,
      });
      if (error) {
        this.err = error.message;
        this.loading = false;
        console.log(error);
      } else {
        this.user = data.user.email;
        setTimeout(() => {
          this.loading = false;
          this.$router.push("/Login");
        }, 2000);

        //this.$router.push("/Login");
      }
    },
  },
};
</script>

<style></style>
