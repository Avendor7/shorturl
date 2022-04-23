<template>
  <v-container>
    <v-row class="text-center">
      <v-col cols="12">
        <h2>ShortURL URL Shortener</h2>
        <p>Created using Vue2, Vuetify, and the shortco.de API</p>
        <v-text-field
            v-model="url"
            :rules="urlRules"
            counter="256"
            hint="https://google.ca"
            label="Shorten URL"
          ></v-text-field>
          <v-btn elevation="2" v-on:click="getURL()">Shorten</v-btn>
      </v-col>
      <h1><a v-bind:href="shortenedURL">{{shortenedURL}}</a></h1>
      
        
    </v-row>
  </v-container>
</template>

<script>

import axios from 'axios';

  export default {
    name: 'ShortURLMainComponent',

    mounted () {
        
    },
    methods: {
      getURL(){
        const url = "https://api.shrtco.de/v2/shorten?url="+ this.url;
        axios.get(url)
          .then(response => {
              //send to the copy thingy
              console.log(response.data.result.full_short_link);
              this.shortenedURL = response.data.result.full_short_link
          })
          .catch(async function (error) {
              const message = {
                  ErrorMessage: error.message,
                  Component: 'CustomerSelectorComponent',
                  APIRoute: url
              }
              alert("Request Failed: " + message.ErrorMessage);
          });
      }
    },
    data () {
      return {
        url: 'https://google.ca',
        description: 'California is a state in the western United States',
        urlRules: [
          v => !!v || 'URL is required',
          v => (v && v.length <= 256) || 'URL must be less than 256 characters', /* eslint-disable-next-line no-useless-escape*/
          v => /https?:[0-9]*\/\/[\w!?/\+\-_~=;\.,*&@#$%\(\)\'\[\]]+/.test(v) || 'URL must be valid',
        ],
        wordsRules: [v => v.trim().split(' ').length <= 5 || 'Max 5 words'],
        shortenedURL:''
      }
    },
  }
</script>
