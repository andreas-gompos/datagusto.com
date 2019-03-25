
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
          v-model="payload.text"
          @input="submit">
        </v-textarea>
      </v-flex>

    </v-layout>
    <v-layout row v-for="(confidence, category) in payload.ClassProbability" :key="category">
      <v-flex xs6 sm4 lg3 >
        <b>{{ category }}: {{confidence.toFixed(1)}}%</b>
        <v-progress-linear height=10 :value="confidence" vertical></v-progress-linear>
      </v-flex>
    </v-layout>


    <v-layout>
      <v-flex xs12 sm6 class="text-xs-center text-sm-left">
        <v-btn outline color="blue darken-2" large @click="limeExplain">Explain</v-btn>
      </v-flex>
    </v-layout>

    <v-layout>
      <v-flex>
        <v-timeline>
          <v-timeline-item
            v-for="(textItem, index) in textArray" :key="index"
            color="red lighten-2"
            small
          >
            <template v-slot:opposite>
              <span>

                <li v-for="(explanation, category) in textItem.limeExplanation" :key="category">
                  {{ category }}: {{explanation}}
                </li>

              </span>
            </template>
            <v-card class="elevation-2">
              <!--//<v-card-title class="headline">Lorem ipsum</v-card-title>/-->
              <v-card-text>
                {{ textItem.text }}
                <li v-for="(confidence, category) in textItem.ClassProbability" :key="category">
                  {{ category }}: {{confidence.toFixed(1)}}%
                </li>
              </v-card-text>
            </v-card>
          </v-timeline-item>
        </v-timeline>
      </v-flex>
    </v-layout>

    <v-layout row>

    </v-layout>
  </v-container>
</template>

<script>
  import axios from 'axios'

  export default {
    name: 'topic_classification',
    data: () => ({
      payload: {
        text: "",
        params: {
          num_features: 5
        },
        ClassProbability: {
          business: 0,
          entertainment: 0,
          politics: 0,
          sport: 0,
          tech: 0,
        },
      },
      textArray: []
    }),
    methods:  {
      submit: function () {
        axios.post('https://services.datagusto.com', this.payload)
          .then(response=>{
            this.payload.ClassProbability.business = parseFloat(response.data.business)
            this.payload.ClassProbability.entertainment = parseFloat(response.data.entertainment)
            this.payload.ClassProbability.politics = parseFloat(response.data.politics)
            this.payload.ClassProbability.sport = parseFloat(response.data.sport)
            this.payload.ClassProbability.tech = parseFloat(response.data.tech)
          })
          .catch(error => console.log(error))

      },
      limeExplain: function () {
        if (this.payload.text==null) {
          console.log('is null')
        } else {
          if (this.payload.text.trim()==='') {
            console.log('is empty')
          } else {
            var tmpArray = {
              'text': this.payload.text,
            }
            axios.post('https://services.datagusto.com', this.payload)
              .then(response=>{
                tmpArray["ClassProbability"] = {
                  "business": parseFloat(response.data.business),
                  "entertainment": parseFloat(response.data.entertainment),
                  "politics": parseFloat(response.data.politics),
                  "sport": parseFloat(response.data.sport),
                  "tech": parseFloat(response.data.tech),
                }
              })
              .catch(error => console.log(error))
            axios.post('https://us-central1-datagusto-core.cloudfunctions.net/bbc-topic-classification-lime-explainer-v1', this.payload)
              .then(response=>{

                tmpArray['limeExplanation'] = response.data
                this.textArray.unshift(tmpArray)
              })
              .catch(error => console.log(error))
          }
        }
      },
    }
  }
</script>
