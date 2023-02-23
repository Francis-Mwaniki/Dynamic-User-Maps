<template>
  <div>
    <!-- sendgrid form to send email content -->
    <div class="flex flex-col justify-center items-center">
      <div class="w-full max-w-xs">
        <form
          class="bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4"
          accept-charset="UTF-8"
          @submit.prevent="onSubmit()"
          method="POST"
        >
          <!-- success div with v-if=success -->
          <div
            v-if="success"
            class="bg-green-100 border border-green-400 text-green-700 px-4 py-3 rounded relative"
            role="alert"
          >
            <strong class="font-bold">Success!</strong>
            <span class="block sm:inline">{{ success }}</span>
          </div>
          <div class="mb-4">
            <label class="block text-gray-700 text-sm font-bold mb-2" for="username">
              Name
            </label>
            <input
              v-model="name"
              class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
              id="username"
              type="text"
              placeholder="Name"
            />
          </div>
          <div class="mb-4">
            <label class="block text-gray-700 text-sm font-bold mb-2" for="username">
              Phone
            </label>
            <input
              v-model="phone"
              class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
              id="username"
              type="text"
              placeholder="Phone"
            />
          </div>

          <div class="mb-4">
            <label class="block text-gray-700 text-sm font-bold mb-2" for="username">
              Email
            </label>
            <input
              v-model="email"
              class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
              id="username"
              type="text"
              placeholder="Email"
            />
          </div>
          <div class="mb-4">
            <label class="block text-gray-700 text-sm font-bold mb-2" for="username">
              Subject
            </label>
            <input
              v-model="subject"
              class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
              id="username"
              type="text"
              placeholder="Subject"
            />
          </div>
          <!-- div for invite-link url input of link  -->
          <div class="mb-4">
            <label class="block text-gray-700 text-sm font-bold mb-2" for="username">
              Invite Link
            </label>
            <input
              v-model="invite_link"
              class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
              id="username"
              type="text"
              placeholder="Invite Link"
            />
          </div>
          <div class="mb-4">
            <label class="block text-gray-700 text-sm font-bold mb-2" for="username">
              Message
            </label>
            <textarea
              v-model="message"
              class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
              id="username"
              type="text"
              placeholder="Message"
            ></textarea>
          </div>
          <div class="flex items-center justify-between">
            <button
              class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
              :class="{ 'opacity-50 cursor-not-allowed': loading }"
              :disabled="loading"
              type="submit"
            >
              {{ loading ? "Sending..." : "Send" }}
            </button>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "SendMail",
  data() {
    return {
      subject: "",
      phone: "",
      loading: false,
      success: "",
      name: "",
      invite_link: "",
      email: "",
      message: "",
      isSuccess: false,
    };
  },
  methods: {
    onSubmit() {
      let data = {
        name: this.name,
        email: this.email,
        message: this.message,
        phone: this.phone,
        invite_link: this.invite_link,
        subject: this.subject,
      };
      this.loading = true;
      fetch("https://getform.io/f/cabd1a3c-a6e1-44da-a47f-4be38e304729", {
        method: "POST",
        headers: {
          Accept: "application/json",
          "Content-Type": "application/json",
        },
        body: JSON.stringify(data),
      })
        .then((response) => response.json())
        .then((data) => {
          // Success
          this.isSuccess = true;
          this.loading = false;
          this.success = "Your message has been sent. Thank you!";
          this.name = "";
          this.email = "";
          this.message = "";
          this.phone = "";
          this.invite_link = "";
          this.subject = "";

          setTimeout(() => {
            this.success = "";
            /* redirect to main */
            this.$router.push("/Main");
          }, 5000);
        })
        .catch((error) => {
          // Error
          console.log(error);
          this.loading = false;
        });
    },
  },
};
</script>

<style scoped></style>
