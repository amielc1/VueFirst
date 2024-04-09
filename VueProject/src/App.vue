<script aetup lang="ts">
import GameVue from "./components/Game.vue";
import HelloWorld from "./components/HelloWorld.vue";
import FormControl from "./components/FormControl.vue";
import Article from "./components/Article.vue";
import Card from "./components/Card.vue";
export default {
  name: "App",
  components: {
    Article,
    FormControl,
    GameVue,
    Card,
  },
  data() {
    let alert = true;
    let apptoken = "Amiel's App Token";
    return { apptoken, alert };
  },
  methods: {
    closePopup(name) {
      this.alert = false;
      console.log("fclose work! " + name);
    },
  },
  provide() {
    return {
      applicationToken: this.apptoken,
    };
  },
};
</script>

<template>
  <v-container>
    <head>
      <link
        href="https://fonts.googleapis.com/css?family=Roboto:300,400,500,700|Material+Icons"
        rel="stylesheet"
      />
    </head>
    <div>
      <a href="https://vitejs.dev" target="_blank">
        <img src="/vite.svg" class="logo" alt="Vite logo" />
      </a>
      <a href="https://vuejs.org/" target="_blank">
        <img src="./assets/vue.svg" class="logo vue" alt="Vue logo" />
      </a>
      <div>
        <v-alert
          v-model="alert"
          border="start"
          variant="tonal"
          closable
          close-label="Close Alert"
          color="deep-purple-accent-4"
          title="Wellcome to my application"
          @close="closePopup"
        >
          {{ this.apptoken }}
        </v-alert>
      </div>
      <card cardTitle="Monday.com" content="How to use monday.com ">
        <v-row > <a href="https://www.youtube.com/watch?v=qFJwsScTwcw">Monday.com toturial</a></v-row>
        <v-row>
          <img
            src="data:image/png;base64,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"
        /></v-row>
      </card>
      <card cardTitle="My second card" content="My content " />
      <card cardTitle="My third card" content="My content " />
       <Article
        title="How Write Vue Components"
        :ispublished="false"
        :rating="3"
        content="In this post we lern how to write a Vue components, "
      />

      <Article
        title="How Write WPF Component"
        :ispublished="true"
        :rating="4"
        content="In this post we lern how to write a WPF components, "
      />
      <FormControl formname="Amiel's Form 1" />
      <GameVue /> 
    </div>
  </v-container>
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
