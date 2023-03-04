<template>
  <v-col cols="auto">
    <v-dialog transition="dialog-top-transition" width="auto">
      <template v-slot:activator="{ props }">
        <v-btn
          v-if="parentProps.add === 0"
          color="primary"
          variant="text"
          v-bind="props"
          @click="formData = { id: 1, fio: '', phone: '', email: '', tags: [] }"
          >+ Add</v-btn
        >
        <v-btn v-else color="warning" variant="text" v-bind="props">
          <v-icon>mdi-pencil</v-icon>
        </v-btn>
      </template>
      <template v-slot:default="{ isActive }">
        <v-card width="400">
          <v-toolbar color="primary" title="Form"></v-toolbar>
          <v-text-field
            v-model="formData.fio"
            label="FIO*"
            persistent-hint
            required
          ></v-text-field>
          <v-text-field
            v-model="formData.phone"
            label="Phone*"
            persistent-hint
            required
          ></v-text-field>
          <v-text-field
            v-model="formData.email"
            type="email"
            label="Email*"
            persistent-hint
            required
          ></v-text-field>
          <v-select
            v-model="formData.tags"
            :items="items"
            chips
            label="Tags"
            multiple
          ></v-select>
          <!-- actions -->
          <v-card-actions class="justify-end">
            <v-btn variant="text" color="error" @click="isActive.value = false"
              >Close</v-btn
            >
            <v-btn variant="text" color="success" @click="submit(isActive)"
              >Save</v-btn
            >
          </v-card-actions>
        </v-card>
      </template>
    </v-dialog>
  </v-col>
</template>

<script lang="ts" setup>
import { ref } from "vue";
import users, { items } from "../service/db/users";

const parentProps = defineProps({
  user_data: Object,
  add: Number,
  edit_function: Function,
  add_function: Function,
});

const dialog = ref(false);
const contacts = ref(users);
const formData = ref({
  id: 1,
  fio: "",
  phone: "",
  email: "",
  tags: [],
  ...parentProps.user_data,
});

function submit(isActive: any) {
  parentProps.add === 0
    ? parentProps?.add_function(formData.value)
    : parentProps?.edit_function(formData.value.id, formData.value);
  isActive.value = false;
}
</script>
