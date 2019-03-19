
<template>
  <v-container fluid>
    <v-layout row>
      <v-flex sm10 lg5>
        <h2 class="headline" >Topic Classifier</h2>
        <v-textarea color="amber" class="mt-3"
          clearable
          auto-grow
          outline
          label="Start typing"
          v-model="article.text"
          @input="submit">
        </v-textarea>
      </v-flex>
    </v-layout>
    <v-layout row v-for="(confidence, category) in ClassProbability" :key="category">
      <v-flex xs6 sm4 lg3 >
        <b>{{ category }}: {{confidence.toFixed(1)}}%</b>
        <v-progress-linear height=10 :value="confidence" vertical></v-progress-linear>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
  import axios from 'axios'

  export default {
    name: 'topic_classification',
    data: () => ({
      article: {
        text: '',
      },
      ClassProbability: {
        business: 0,
        entertainment: 0,
        politics: 0,
        sport: 0,
        tech: 0,
      }
    }),
    methods:  {
      submit: function () {
        axios.post('https://services.datagusto.com', this.article)
          .then(response=>{
            this.ClassProbability.business = parseFloat(response.data.business)
            this.ClassProbability.entertainment = parseFloat(response.data.entertainment)
            this.ClassProbability.politics = parseFloat(response.data.politics)
            this.ClassProbability.sport = parseFloat(response.data.sport)
            this.ClassProbability.tech = parseFloat(response.data.tech)
          })
          .catch(error => console.log(error))

      },
      clear () {
        this.article.text = ""
      }
    }
  }
</script>
