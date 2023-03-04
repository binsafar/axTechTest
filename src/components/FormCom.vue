<template>
  <v-col cols="auto">
    <v-dialog transition="dialog-top-transition" width="auto">
      <template v-slot:activator="{ props }">
        <v-btn v-if="add" color="primary" variant="text" v-bind="props"
          >+ Add</v-btn
        >
        <v-btn v-else color="warning" variant="text" v-bind="props">
          <v-icon>mdi-pencil</v-icon>
        </v-btn>
      </template>
      <template v-slot:default="{ isActive }">
        <v-card width="400">
          <v-toolbar color="primary" title="Form"></v-toolbar>
          <v-text-field label="FIO*" persistent-hint required></v-text-field>
          <v-text-field label="Phone*" persistent-hint required></v-text-field>
          <v-text-field label="Email*" persistent-hint required></v-text-field>
          <v-select
            v-model="contacts[0].tags"
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
            <v-btn
              variant="text"
              color="success"
              @click="isActive.value = false"
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

const dialog = ref(false);
const contacts = ref(users);

defineProps({
  user: Object,
  add: Boolean,
});
</script>
