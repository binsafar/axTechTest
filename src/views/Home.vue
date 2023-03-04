<template>
  <v-container>
    <v-table density="compact">
      <thead>
        <tr>
          <th class="text-left">N</th>
          <th class="text-left">FIO</th>
          <th class="text-left">Phone</th>
          <th class="text-left">Email</th>
          <th class="text-left">Tags</th>
          <form-com :add="true" />
        </tr>
      </thead>

      <tbody>
        <tr v-for="(contact, index) in contacts" :key="contact.id">
          <td>{{ index + 1 }}</td>
          <td>{{ contact.fio }}</td>
          <td>{{ contact.phone }}</td>
          <td>{{ contact.email }}</td>
          <td class="d-flex align-center justify-space-between fill-height">
            <v-select
              v-model="contact.tags"
              :items="items"
              chips
              label="Tags"
              multiple
              disabled
            ></v-select>
          </td>
          <td>
            <div class="d-flex align-center">
              <form-com :user_data="contact" :add="false" />
              <v-btn
                variant="text"
                color="error"
                @click="deleteContact(contact.id)"
              >
                <v-icon> mdi-delete </v-icon>
              </v-btn>
            </div>
          </td>
        </tr>
      </tbody>
    </v-table>
  </v-container>
</template>

<script lang="ts" setup>
import FormCom from "@/components/FormCom.vue";
import { onBeforeMount } from "vue";
import router from "@/router";
import { ref } from "vue";
import users, { items } from "../service/db/users";

const contacts = ref(users);

const deleteContact = (id: number) => {};

onBeforeMount(() => {
  let status = localStorage.getItem("status");
  if (status !== "logged") router.push("/");
});
</script>
