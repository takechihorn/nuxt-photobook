<template>
  <div>
    <ul class="flex justify-end">
      <li class="mr-6" v-if="!user">
        <nuxt-link to="/">
          <a class="text-blue-500 hover:text-blue-800 cursor-pointer">Login</a>
        </nuxt-link>
      </li>
      <li class="mr-6" v-if="!user">
        <nuxt-link to="/register">
          <a class="text-blue-500 hover:text-blue-800 cursor-pointer"
            >Sign Up</a
          >
        </nuxt-link>
      </li>
      <li class="mr-6" v-if="user">
        <div class="font-semibold text-black-500">
          Welcome {{ user.username }}
        </div>
      </li>
      <li class="mr-6" v-if="user">
        <nuxt-link to="/albums">
          <div class="text-blue-500 hover:text-blue-800 cursor-pointer">
            Albums
          </div>
        </nuxt-link>
      </li>
      <li class="mr-6" v-if="user">
        <div
          class="text-blue-500 hover:text-blue-800 cursor-pointer"
          @click="logout"
        >
          Logout
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  methods: {
    async logout() {
      await this.$store.dispatch("auth/logout");
      this.$router.push("/");
    }
  },
  computed: {
    user() {
      return this.$store.getters.user;
    }
  }
};
</script>

<style>
</style>
