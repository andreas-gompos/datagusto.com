<template>
    <v-container fluid>
        <v-layout justify-center row wrap>
            <v-flex lg7>
                <v-card color="blue-grey" class="white--text">
                    <v-container fluid>
                        <v-layout justify-left row>
                            <v-flex xs12>
                                <v-card-title primary-title>
                                    <div>
                                        <h3 class="headline">Topic Classifier</h3>
                                        <div>Classify text into tech, politics, sports, entertainment or business.</div>
                                    </div>
                                </v-card-title>
                            </v-flex>
                        </v-layout>
                        <v-layout row>
                            <v-card-actions>
                                <v-btn  to="/models/topic_classification" color="amber">GO TO DEMO</v-btn>
                                <v-btn href="https://github.com/andreas-gompos/ml-apps/tree/master/topic_classification_app" target="_blank" flat icon>
                                    <v-icon class="blue-grey--text text--lighten-5" light>fab fa-github</v-icon>
                                </v-btn>
                            </v-card-actions>
                        </v-layout>
                    </v-container>
                </v-card>
            </v-flex>
        </v-layout>
    </v-container>
</template>