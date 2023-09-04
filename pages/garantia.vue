<template>
  <v-container>
    <h2 class="d-flex justify-center mt-5 mb-7">
      Ordens de serviço na garantia
    </h2>

    <v-container class="justify-center">
      <div v-for="(group, day) in groupedCards" :key="day">
        <v-card-title class="mb-3">{{ formatData(day) }}</v-card-title>

        <v-card
          v-for="item in group"
          :key="item.os"
          width="100%"
          height="200"
          class="mb-5 align-center justify-center"
          elevation="1"
          color="grey lighten-3"
        >
          <v-card-title>
            <v-chip class="mt-3 ml-3" label>OS.{{ item.os }}</v-chip>
            <v-spacer></v-spacer>
            <v-chip class="mt-3 mr-3">{{ item.horario }}</v-chip>
          </v-card-title>

          <v-card-subtitle class="ml-3 mt-4 text-black subtitle-1">
            Tipo: {{ item.tipo }} <br />
            Empresa: {{ item.cliente }}
          </v-card-subtitle>

          <v-card-text></v-card-text>
        </v-card>
      </div>
    </v-container>
  </v-container>
</template>
  
  <script>
import moment from 'moment'
import 'moment/locale/pt-br'

export default {
  name: 'OsNaGarantia',
  data() {
    return {
      listaOs: [
        {
          os: '00001',
          tipo: 'Instalação',
          data: '2023-08-01',
          cliente: 'Selbetti',
          horario: '16:30',
        },
        {
          os: '00002',
          tipo: 'Instalação',
          data: '2023-07-25',
          cliente: 'FVB Locadora',
          horario: '08:00',
        },
        {
          os: '00003',
          tipo: 'Instalação',
          data: '2023-09-29',
          cliente: 'Tinto Max',
          horario: '18:00',
        },
        {
          os: '00004',
          tipo: 'Instalação',
          data: '2023-05-29',
          cliente: 'Selbetti',
          horario: '14:00',
        },
        {
          os: '00005',
          tipo: 'Instalação',
          data: '2023-05-29',
          cliente: 'Selbetti',
          horario: '15:00',
        },
      ],

      today: moment(),
    }
  },
  computed: {
    groupedCards() {
      return this.groupCardsByDay()
    },
  },
  methods: {
    groupCardsByDay() {
      // Filtrar a lista de OS para os últimos 31 dias
      const date31DaysAgo = moment().subtract(31, 'days')
      const filteredList = this.listaOs.filter((item) => {
        const osDate = moment(item.data)
        return osDate.isSameOrAfter(date31DaysAgo, 'day')
      })

      const sortedList = filteredList.sort((a, b) => {
        return moment(a.data).valueOf() - moment(b.data).valueOf()
      })

      const groupedCards = {}

      sortedList.forEach((item) => {
        const date = item.data
        if (!groupedCards[date]) {
          groupedCards[date] = []
        }
        groupedCards[date].push(item)
      })

      return groupedCards
    },

    formatData(date) {
      return moment(date).format('DD/MM/YYYY')
    },
  },
}
</script>
  
  <style>
</style>
  