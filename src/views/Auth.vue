<script lang="ts">
import router from "@/router";
import { ref } from "vue";

export {};

let username = ref({ value: "" });
let password = ref({ value: "" });

const loginProcess = () => {
  if (username.value.value === "admin" && password.value.value === "admin") {
    router.push("/home");
    return false;
  } else return true;
};
</script>

<template>
  <v-card class="mx-auto root-wrapper" width="400">
    <h1 class="text-center">Authentication</h1>
    <form class="mx-auto" @submit.prevent="">
      <v-form fast-fail @submit.prevent>
        <v-text-field v-model="username" label="Username"></v-text-field>

        <v-text-field
          v-model="password"
          label="Password"
          type="password"
        ></v-text-field>

        <v-btn type="submit" block class="mt-2">Submit</v-btn>
      </v-form>
    </form>
  </v-card>
</template>

<style scoped>
.root-wrapper {
  margin-top: 15%;
}
</style>
