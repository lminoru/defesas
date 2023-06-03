<template>
  <v-container class="light-grey fill-height">
    <v-row class="text-center">

      <v-col class="mb-4" cols="12">
        <h1 class="display-2 font-weight-bold mb-3">
          Pós-Graduação
        </h1>
      </v-col>
    </v-row>
    <v-row justify="center">
      <v-btn>Acessar defesas</v-btn>
    </v-row>

    <v-row>
      <v-col cols="2" class="mx-auto" v-for="autor in autores" :key="autor.uspNumber">
        <CardAutor :key="autor.uspNumber" :autor="autor" />
      </v-col>
    </v-row>

  </v-container>
</template>

<script>
import CardAutor from './CardAutor.vue'

export default {
  name: 'Menu',

  components: {
    CardAutor
  },

  data: () => ({
    autores: [
      {
        name: 'Leonardo Minoru Iwashima',
        uspNumber: '12534738',
        imageName: 'minoru.png'
      },
      {
        name: 'Ueslei Aparecido Pina',
        uspNumber: '11837081',
        imageName: 'ueslei.png'
      },
      {
        name: 'Nicolas de Góes',
        uspNumber: '12563780',
        imageName: 'nicolas.png'
      }
    ]
  })
}
</script>
