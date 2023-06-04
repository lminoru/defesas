<template>
  <div>
    <template v-if="loading">
      <v-dialog v-model="loading">
        <v-card>
          <v-progress-linear indeterminate color="primary"></v-progress-linear>
        </v-card>
      </v-dialog>
    </template>
    <template v-if="defesas.length !== 0">
      <!-- input para filtragem por nome -->
      <v-text-field type="text" v-model="search" append-icon="mdi-magnify" label="Digite um nome"
        single-line></v-text-field>

      <!-- Coluna com radio buttons para filtragem -->
      <v-radio-group v-model="filters.curso" row>
        <v-radio v-for="c in cursoOptions" :key="c.text" :label="c.text" :value="c.value"></v-radio>
      </v-radio-group>

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
  name: 'Defesas',
  data() {
    return {
      personagem: undefined,
      cnt: 0,
      search: '',
      headers: [
        {
          text: 'Curso',
          value: 'Curso',
          filter: value => {
            if (!this.filters.curso) return true

            return value === this.filters.curso
          }
        },
        { text: 'Programa', value: 'Programa', filterable: false },
        { text: 'Ordem', value: 'Ordem', filterable: false },
        { text: 'Nome', value: 'Nome' },
        { text: 'Data', value: 'Data', filterable: false }
      ],
      defesas: [],
      loading: false,
      sortBy: 'Data',
      sortDesc: false,
      filters: {
        nome: '',
        curso: ''
      },
      cursoOptions: [
        { text: 'Mestrado', value: 'Mestrado' },
        { text: 'Doutorado', value: 'Doutorado' },
        { text: 'DD', value: 'DD' },
        { text: 'Nenhum', value: '' }
      ]
    },
      created() {
      this.loadDefesas()
    },
    methods: {
      loadDefesas() {
        this.loading = true
        const url = 'http://thanos.icmc.usp.br:4567/api/v1/defesas'
        fetch(url)
          .then((data) => (data.json()))
          .then((response) => {
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
