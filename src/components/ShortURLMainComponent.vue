<template>
  <v-container>
    <v-row class="text-center">
      <v-col cols="12">
        <h2>ShortURL URL Shortener</h2>
        <p>Created using Vue2, Vuetify, and the shortco.de API</p>
        <v-text-field
            v-model="title"
            :rules="rules"
            counter="25"
            hint="This field uses counter prop"
            label="Shorten URL"
          ></v-text-field>
          <v-btn elevation="2">Shorten</v-btn>
      </v-col>

      
        
    </v-row>
  </v-container>
</template>

<script>

//import axios from 'axios';

  export default {
    name: 'ShortURLMainComponent',

    mounted () {
        
    },

    data () {
      return {
        title: 'URL',
        description: 'California is a state in the western United States',
        rules: [v => v.length <= 25 || 'Max 25 characters'],
        wordsRules: [v => v.trim().split(' ').length <= 5 || 'Max 5 words'],
      }
    },
  }
</script>
