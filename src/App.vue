<template>
  <v-app dark>
    <v-app-bar
      app
      color="primary"
      dark
    >
      <div class="d-flex align-center">
        <h1>URL Shortener</h1>
      </div>
      <v-spacer></v-spacer>

      <v-btn
        href="https://github.com/Avendor7/shorturl"
        target="_blank"
        text
      >
        <span class="mr-2">GitHub</span>
        <v-icon>mdi-open-in-new</v-icon>
      </v-btn>
    </v-app-bar>

    <v-main>
      <ShortURLMainComponent/>
    </v-main>
  </v-app>
</template>

<script>
import ShortURLMainComponent from './components/ShortURLMainComponent.vue';

export default {
  name: 'App',

  components: {
    ShortURLMainComponent,
  },
  data: () => ({
    //
  }),
};
</script>
