<template>
  <div>
    <form
      v-if="step === steps.register"
      class="flex flex-col items-center"
      @submit.prevent="register"
    >
      <div class="flex flex-col user">
        <label class="block text-gray-700 text-sm font-bold mb-2" for="username"
          >User Name</label
        >
        <input
          class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
          type="name"
          v-model="registerForm.username"
          placeholder="UserName"
          id="userName"
        />
      </div>
      <div class="flex flex-col mt-2">
        <label class="block text-gray-700 text-sm font-bold" for="email"
          >Email</label
        >
        <input
          class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 mb-3 leading-tight focus:outline-none focus:shadow-outline"
          type="email"
          id="email"
          v-model="registerForm.email"
          placeholder="Email"
        />
      </div>
      <div class="flex flex-col mt-2">
        <label class="block text-gray-700 text-sm font-bold mb-2" for="password"
          >Password</label
        >
        <input
          class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 mb-3 leading-tight focus:outline-none focus:shadow-outline"
          type="password"
          id="password"
          v-model="registerForm.password"
          placeholder="Password"
        />
      </div>

      <!-- eslint-disable -->
      <button class="btn-blue">Register</button>
    </form>
    <form v-else @submit.prevent="confirm">
      <div class="flex flex-col mt-2">
        <label class="block text-gray-700 text-sm font-bold" for="email"
          >ConfirmEmail</label
        >
        <input
          class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 mb-3 leading-tight focus:outline-none focus:shadow-outline"
          type="email"
          id="email"
          v-model="confirmForm.email"
          placeholder="Email"
        />
      </div>
      <div class="flex flex-col mt-2">
        <label class="block text-gray-700 text-sm font-bold mb-2" for="password"
          >Code</label
        >
        <input
          class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 mb-3 leading-tight focus:outline-none focus:shadow-outline"
          type="code"
          id="code"
          v-model="confirmForm.code"
          placeholder="code"
        />
        <button class="btn-blue" type="submit">Confirm Code</button>
      </div>
    </form>
  </div>
</template>

<script>
const steps = {
  register: "REGISTER",
  confirm: "CONFIRM"
};
export default {
  data: () => ({
    steps: { ...steps },
    step: steps.register,
    registerForm: {
      username: "",
      email: "",
      password: ""
    },
    confirmForm: {
      email: "",
      code: ""
    }
  }),
  methods: {
    async register() {
      try {
        await this.$store.dispatch("auth/register", this.registerForm);
        this.confirmForm.email = this.registerForm.email;
        this.step = this.steps.confirm;
      } catch (error) {
        console.log({ error });
      }
    },
    async confirm() {
      try {
        await this.$store.dispatch(
          "auth/confirmRegistration",
          this.confirmForm
        );
        await this.$store.dispatch("auth/login", this.registerForm);
        this.$router.push("/");
      } catch (error) {
        console.log({ error });
      }
    }
  }
};
</script>

<style>
</style>
