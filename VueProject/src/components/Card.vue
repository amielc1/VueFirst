<template>
  <v-container>
    <v-layout justify-center>
      <div>
        <v-card :title="cardTitle" :subtitle="Date().toLocaleString()"  :text="content">
           <slot></slot>
        </v-card>
      </div>
    </v-layout>
  </v-container>
</template>

<script lang="ts">
import Vue from "vue";
export default {
  name: "Card",
  inject: [],
  emits: [],
  props: {
    content: String,
    cardTitle: String,
    ispublished: Boolean,
  },
  data() {
    return {};
  },
  methods: {},
};
</script>

<style scoped></style>
