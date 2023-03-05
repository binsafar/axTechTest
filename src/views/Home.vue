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
          <form-com
            :add="0"
            :add_function="addContact"
            :edit_function="editContact"
          />
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
              <form-com
                :user_data="contact"
                :add_function="addContact"
                :edit_function="editContact"
                :add="1"
              />
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
import { onBeforeMount, ref } from "vue";
import FormCom from "@/components/FormCom.vue";
import router from "@/router";
import users, { items } from "../service/db/users";

const contacts = ref(users);

const deleteContact = (id: number) => {
  let index = contacts.value.findIndex((item) => item.id === id);
  contacts.value.splice(index, 1);
};

const addContact = (user: any) => {
  if (contacts.value.length != 0) {
    contacts.value.push({
      ...user,
      id: contacts.value[contacts.value.length - 1].id + 1,
    });
  } else contacts.value.push({ ...user, id: 1 });
};

const editContact = (id: number, user: any) => {
  let index = contacts.value.findIndex((item) => item.id === id);
  contacts.value[index] = { ...user, id };
};

onBeforeMount(() => {
  let status = localStorage.getItem("status");
  if (status !== "logged") router.push("/");
});
</script>
