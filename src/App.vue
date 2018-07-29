<template>
<div>
    <v-app>
    <main>
      <topic-classification-model></topic-classification-model>
    </main>
    </v-app>

  </div>
</template>

<script>
import TopicClassificationModel from './components/TopicClassificationModel'

export default {
  name: 'app',
  components: {
    TopicClassificationModel
  }
}
</script>

<style>

</style>
