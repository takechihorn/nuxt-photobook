<template>
  <div>
    <div v-if="!$auth.isAuthenticated">
      <form class="flex flex-col items-center" @submit.prevent="login">
        <div class="flex flex-col user">
          <label
            class="block text-gray-700 text-sm font-bold mb-2"
            for="username"
            >User Name</label
          >
          <input
            class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
            type="text"
            v-model="username"
            id="userName"
          />
        </div>
        <div class="flex flex-col user">
          <label class="block text-gray-700 text-sm font-bold mb-2" for="email"
            >Email</label
          >
          <input
            class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
            type="email"
            v-model="email"
            id="Email"
          />
        </div>
        <div class="flex flex-col mt-10">
          <label
            class="block text-gray-700 text-sm font-bold mb-2"
            for="password"
            >Password</label
          >
          <input
            class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 mb-3 leading-tight focus:outline-none focus:shadow-outline"
            type="password"
            v-model="password"
          />
        </div>
        <!-- eslint-disable -->
        <button class="btn-blue">Sign in</button>
      </form>
    </div>
    <div class="text-red-600">{{ error.message }}</div>
  </div>
</template>

<script>
export default {
  data: () => ({
    username: "",
    password: "",
    email: "",
    error: ""
  }),
  methods: {
    async login() {
      try {
        await this.$store.dispatch("auth/login", {
          username: this.username,
          email: this.email,
          password: this.password
        });
        this.$router.push("/albums");
      } catch (error) {
        console.log(error);
        this.error = error;
      }
    }
  }
};
</script>

<style>
</style>
