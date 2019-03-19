<template>

  <v-container fluid>
    <v-layout column>
        <v-flex>
            <h1>explore. interpret. learn.</h1>
        </v-flex>
        <v-flex>
            <h1 class="blue--text text--darken-2">taste what data can do.</h1>
        </v-flex>
    </v-layout>

    <v-layout row wrap>
        <p>Datagusto hosts a collection of interactive demos of
            machine learning applications on different domains.
        </p>
    </v-layout>


    <v-layout row wrap>
        <v-flex xs12 sm6 class="text-xs-center text-sm-right">
            <v-btn color="blue darken-3" dark large to="/models" >Explore the Models</v-btn>
        </v-flex>
        <v-flex xs12 sm6 class="text-xs-center text-sm-left">
            <v-btn outline color="blue darken-2" large to="/blog">Read the Blog</v-btn>
        </v-flex>
    </v-layout>

  </v-container>
</template>

<script>

export default {
  components: {
  }
}
</script>
