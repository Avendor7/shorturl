<template>
  <div>
    <v-container>
      <v-row align="center" justify="center">
        <v-col>
          <v-text-field
              ref="form"
              v-model="url"
              :rules="urlRules"
              counter="256"
              label="Shorten URL"
            ></v-text-field>
            <v-btn elevation="2" v-on:click="getURL()">Shorten</v-btn>
        </v-col>
        
      </v-row>
      <v-row align="center" justify="center">
        <v-col class="d-flex justify-center">
          <div v-show="shortenedURL">
            <v-text-field v-on:focus="$event.target.select()" ref="shorturl" v-bind:value="shortenedURL"></v-text-field>
            <v-btn elevation="2" v-on:click="copyToClipboard()">Copy to Clipboard</v-btn>
        </div>
        </v-col>
      </v-row>
    
    </v-container>
    <v-footer bottom fixed>
      <v-col
        class="text-center"
        cols="12"
      >
      Created using Vue2, Vuetify, and the <a href="https://shrtco.de" target="_blank">shrtco.de</a> API
      </v-col>
    </v-footer>
  </div>
</template>

<script>

import axios from 'axios';

  export default {
    name: 'ShortURLMainComponent',

    mounted () {
        
    },
    methods: {
      getURL(){
        
        if (this.$refs.form.validate()){
          const url = "https://api.shrtco.de/v2/shorten?url="+ this.url;
          axios.get(url)
            .then(response => {
              if (response.data.result.error_code){
                alert(response.data.result.error_code);
              }else{
                this.shortenedURL = response.data.result.full_short_link;
              }
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
      copyToClipboard(){
        this.$refs.shorturl.focus();
        document.execCommand('copy');
      }
    },
    data () {
      return {
        url: null,
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
