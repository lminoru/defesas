<template>
  <div>
    <v-btn :loading="loading" class="primary" @click="loadDefesas()">Load!</v-btn>

    <v-text-field v-model="search" append-icon="mdi-magnify" label="Digite um nome" single-line
      hide-details></v-text-field>

    <template v-if="defesas.length !== 0">
      <v-data-table :headers="headers" :items="defesas" class="elevation-1" :loading="loading" :search="search">
        <template v-slot:[`item.Data`]="{ item }">
          {{ formatDate(item.Data) }}
        </template>
        <template v-slot:[`item.Curso`]="{ item }">
          {{ formatCourse(item.Curso) }}
        </template>
      </v-data-table>
    </template>
  </div>
</template>

<script>

export default {
  components: {
  },
  name: 'GotView',
  data() {
    return {
      personagem: undefined,
      cnt: 0,
      search: '',
      headers: [],
      defesas: [],
      regrasNome: [
        (value) => (value.length >= 3) || 'Digite ao menos 3 letras',
        (value) => (value !== 'Drogo') || 'Drogo nao por favor!!'
      ],
      loading: false,
      sortBy: 'Data',
      sortDesc: false
    }
  },
  methods: {
    loadDefesas() {
      this.loading = true
      const url = 'http://thanos.icmc.usp.br:4567/api/v1/defesas'
      fetch(url)
        .then((data) => (data.json()))
        .then((response) => {
          this.headers = response.hs
          this.defesas = this.formatItems(response.items)
          this.loading = false
        })
    },
    formatCourse(courseString) {
      if (courseString === 'ME') {
        return 'Mestrado'
      } else if (courseString === 'DO') {
        return 'Doutorado'
      }
      return courseString
    },
    formatDate(dateString) {
      // Implemente a lógica para formatar a data no formato DD/MM/AAAA
      const [year, month, day] = dateString.split('-')
      const date = `${day}/${month}/${year}`
      return date
    },
    formatDateForSorting(dateString) {
      const [day, month, year] = dateString.split('/')
      const isoDate = `${year}-${month}-${day}`
      return isoDate
    },
    formatItems(data) {
      return data.map((item) => ({
        ...item,
        Data: this.formatDateForSorting(item.Data),
        Curso: this.formatCourse(item.Curso)
      }))
    }
  }
}
</script>
