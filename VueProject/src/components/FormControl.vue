<script lang="ts">
import { ref } from "vue";

export default {
  props : ['formname'],
  data() {
    let name = "FormControl";
    let valid = false;
    let contries = [
      "California",
      "Colorado",
      "Florida",
      "Georgia",
      "Texas",
      "Wyoming",
    ];
    let formvalues = {
      firstname: "",
      lastname: "",
      email: "",
      selectedCounry: "",
      isworkFromHome: false,
      skills: [],
      yearsofexperience: "",
      age: 0,
    };
    let nameRules = [
      (value) => {
        if (value) return true;

        return "Name is required.";
      },
      (value) => {
        if (value?.length <= 10) return true;

        return "Name must be less than 10 characters.";
      },
    ];

    let emailRules = [
      (value) => {
        if (value) return true;

        return "E-mail is requred.";
      },
      (value) => {
        if (/.+@.+\..+/.test(value)) return true;

        return "E-mail must be valid.";
      },
    ];
    return {
      valid,
      contries,
      nameRules,
      emailRules,
      formvalues,
      name,
    };
  },
  methods: {
    submitform(event) {
      event.preventDefault();
      console.log("form values : ", this.formvalues);
    },
  },
};
</script>

<template>
  <v-container>
    <v-layout justify-center>
      <v-form  v-model="valid">
        <v-container>
          <h2>{{formname}}</h2>
          <v-row>{{ JSON.stringify(formvalues, null, 2) }}</v-row>
          <v-row>
            <v-col cols="12" md="4">
                <v-text-field
                  v-model.trim.lazy="formvalues.firstname"
                  :rules="nameRules"
                  :counter="10"
                  label="First name"
                  required
                  hide-details
                ></v-text-field>
            </v-col>

            <v-col cols="12" md="4">
              <v-text-field
                v-model.trim.lazy="formvalues.lastname"
                :rules="nameRules"
                :counter="10"
                label="Last name"
                hide-details
                required
              ></v-text-field>
            </v-col>

            <v-col cols="12" md="4">
              <v-text-field
                v-model.trim.lazy="formvalues.email"
                :rules="emailRules"
                label="E-mail"
                hide-details
                required
              ></v-text-field>
            </v-col>
            <v-col cols="12" md="4">
              <v-select
                label="Job Locations"
                multiple
                v-model="formvalues.selectedCounry"
                :items="contries"
              ></v-select>
            </v-col>
          </v-row>
          <v-row>
            <v-col cols="12" md="4">
              <v-checkbox
                type="checkbox"
                v-model="formvalues.isworkFromHome"
                label="Work from home ? "
              ></v-checkbox>
            </v-col>
          </v-row>
          <v-row>
            <v-checkbox
              type="checkbox"
              v-model="formvalues.skills"
              label="C#"
              value="C#"
            ></v-checkbox>
            <v-checkbox
              type="checkbox"
              v-model="formvalues.skills"
              value="Java"
              label="Java"
            ></v-checkbox>
            <v-checkbox
              type="checkbox"
              v-model="formvalues.skills"
              label="Vue.js"
              value="Vue.js"
            ></v-checkbox>
          </v-row>
          <v-row>
            <v-radio-group inline label="Years of experience">
              <v-radio
                v-model="formvalues.yearsofexperience"
                label="0-2"
                value="0-2"
              ></v-radio>
              <v-radio
                v-model="formvalues.yearsofexperience"
                label="3-5"
                value="3-5"
              ></v-radio>
              <v-radio
                v-model="formvalues.yearsofexperience"
                label="5-10"
                value="5-10"
              ></v-radio>
            </v-radio-group>
          </v-row>
          <v-row>
            <v-btn type="submit" @click="submitform" class="mt-2">Submit</v-btn>
          </v-row>
        </v-container>
      </v-form>
    </v-layout>
  </v-container>
</template>

<style scoped></style>
