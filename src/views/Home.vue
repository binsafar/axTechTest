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
          <th class="text-left"><v-btn variant="text">+ add</v-btn></th>
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
            <div>
              <v-btn variant="text">
                <v-icon> mdi-pencil </v-icon>
              </v-btn>

              <v-btn variant="text" @click="deleteContact(contact.id)">
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
import { ref } from "vue";

let items = ["home", "office", "family", "friends"];
const contacts = ref([
  {
    id: 1,
    fio: "John Doe",
    phone: "90 123 23 23",
    email: "doe@gmail.com",
    tags: ["office"],
  },
  {
    id: 2,
    fio: "John Deo",
    phone: "90 123 22 22",
    email: "doe@outlook.com",
    tags: ["office"],
  },
  {
    id: 3,
    fio: "Doe John",
    phone: "90 123 11 11",
    email: "doe@mail.ru",
    tags: ["office"],
  },
]);
const deleteContact = (id: number) => {
  contacts.value.slice(id, 1);
};
</script>
