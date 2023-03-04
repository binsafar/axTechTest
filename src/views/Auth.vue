<template>
  <v-card class="mx-auto root-wrapper" width="400">
    <h1 class="text-center">Authentication</h1>
    <form class="mx-auto" @submit.prevent="loginProcess">
      <v-form fast-fail @submit.prevent>
        <v-text-field
          v-model="userData.username"
          label="Username"
        ></v-text-field>

        <v-text-field
          v-model="userData.password"
          label="Password"
          type="password"
        ></v-text-field>

        <v-btn @click="loginProcess" type="submit" block class="mt-2"
          >Submit</v-btn
        >
      </v-form>
    </form>
  </v-card>
</template>

<script lang="ts" setup>
import router from "@/router";
import { ref, onMounted } from "vue";

let userData = ref({ username: "", password: "" });
onMounted(() => {
  localStorage.clear();
});
const loginProcess = () => {
  if (
    userData.value.username === "admin" &&
    userData.value.password === "admin"
  ) {
    localStorage.clear();
    localStorage.setItem("status", "logged");
    router.push("/home");
  } else alert("Username: admin, Password: admin");
};
</script>

<style scoped>
.root-wrapper {
  margin-top: 15%;
}
</style>
