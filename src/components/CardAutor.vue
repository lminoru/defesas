<template>
  <v-card class="black--text my-12">
    <v-card-avatar>
      <v-img contain :src="require(`../assets/${autor.imageName}`)" height="100"></v-img>
    </v-card-avatar>

    <v-card-title class="text-truncate">{{ autor.name }}</v-card-title>

    <v-card-text>
      <p>Número USP: {{ autor.uspNumber }}</p>
    </v-card-text>
  </v-card>
</template>

<script>
export default {
  props: ['autor']
}
</script>
