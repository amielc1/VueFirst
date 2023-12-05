<template>
  <v-container>
    <v-layout justify-center>
      <v-col>
        <h2>{{ title }}</h2>
        <v-row> 
          <v-rating
            hover
            :length="5"
            :size="32"
            :model-value="rating"
            active-color="primary"
        /></v-row>
        <v-row>
          <v-chip class="ma-2" :color="ispublished ? 'green' : 'red'" label>
            <v-icon start icon="mdi-label"></v-icon>
            {{ ispublished ? "Published" : "Wait to publish" }}
          </v-chip>
          <v-chip class="ma-2" color="orange" label>
            <v-icon start icon="mdi-label"></v-icon>
            {{ applicationToken }}
          </v-chip>
        </v-row>
        <v-row>
          <p>{{ content }}</p>
        
          </v-row>
          <!-- close App popup by emit event  -->
          <v-row> <v-btn @click="$emit('close','apppopup')">Close</v-btn></v-row>
         
      </v-col>
    </v-layout>
  </v-container>
</template>

<script lang="ts">
import Vue from "vue";

export default {
  name: "Article",
  inject: ["applicationToken"],
  emits:['close'],
  props: {
    title: {
      type: String,
      required: true,
      default: "Default Title Post",
    },
    content: String,
    rating: Number,
    ispublished: Boolean,
  },
  data() {
    return {};
  },
  methods: {},
};
</script>

<style scoped></style>
