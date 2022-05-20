<template>
  <div>
    <h3>Account Information</h3>
    <form @submit.prevent="infoSubmit">
      <div class="mb-3">
        <v-text-field v-model="user.first_name" label="First name" />
      </div>
      <div class="mb-3">
        <v-text-field v-model="user.last_name" label="Last name" />
      </div>
      <div class="mb-3">
        <v-text-field v-model="user.email" type="email" label="Email" />
      </div>
      <v-btn color="primary" type="submit">Save</v-btn>
    </form>

    <h3 class="mt-4" @submit.prevent="passwordSubmit">Change password</h3>
    <form>
      <div class="mb-3">
        <v-text-field v-model="password" label="Password" />
      </div>
      <div class="mb-3">
        <v-text-field v-model="password_confirm" label="Password confirmation" />
      </div>
      <v-btn color="primary" type="submit">Save</v-btn>
    </form>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Profile",
  data() {
    return {
      password: "",
      password_confirm: "",
    };
  },
  methods: {
    async infoSubmit() {
      const { data } = await axios.put("users/info", {
        first_name: this.user.first_name,
        last_name: this.user.last_name,
        email: this.user.email,
      });

      await this.$store.dispatch("setUser", data);
    },
    async passwordSubmit() {
      await axios.put("users/password", {
        password: this.password,
        password_confirm: this.password_confirm,
      });
    },
  },
  computed: {
    user() {
      return this.$store.state.user;
    },
  },
};
</script>

<style></style>
