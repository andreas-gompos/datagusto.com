<template>
  <v-container fluid grid-list-md>
    <h2 align="center">Article Classifier</h2>
    <v-textarea color="red"
                name="input-7-1"
                label="Start typing"
                clearable="true"
                v-model="article.text"
                @keyup="submit">
    </v-textarea>
    <v-btn color="red" @click="submit">Submit</v-btn>
    <v-container fluid grid-list-md >
      <v-layout row wrap v-for="(confidence, category) in ClassProbability">
        <v-flex xs6>
          <b>{{ category }}:</b>
          <v-progress-linear height=10 :value="confidence"></v-progress-linear>
        </v-flex>
      </v-layout>
    </v-container>
  </v-container>
</template>

<script>
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
        if (this.article.text.trim() === '') {
          this.ClassProbability.business = 0
          this.ClassProbability.entertainment = 0
          this.ClassProbability.politics = 0
          this.ClassProbability.sport = 0
          this.ClassProbability.tech = 0
        } else {
       this.$http.post('http://topic_classification.models.datagusto.com', this.article).then(response => {
          this.ClassProbability.business = parseFloat(response.body.business)
          this.ClassProbability.entertainment = parseFloat(response.body.entertainment)
          this.ClassProbability.politics = parseFloat(response.body.politics)
          this.ClassProbability.sport = parseFloat(response.body.sport)
          this.ClassProbability.tech = parseFloat(response.body.tech)
          });
      }
      }
    }
  }
</script>
