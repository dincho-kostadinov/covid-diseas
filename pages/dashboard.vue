<template>
    <v-data-table
    :headers="headers"
    :items="countries"
    :items-per-page="15"
    class="elevation-1"
  ></v-data-table>
</template>

<script>
const axios = require('axios');
export default {
    data () {
      return {
        headers: [
          {
            text: 'Country',
            align: 'start',
            sortable: false,
            value: 'country',
          },
          { text: 'Total cases', value: 'cases' },
          { text: 'New Cases', value: 'todayCases' },
          { text: 'Carbs (g)', value: 'carbs' },
          { text: 'Protein (g)', value: 'protein' },
          { text: 'Iron (%)', value: 'iron' },
        ],
        countries:[],
      }
    },
   created() {
    axios.get(`https://disease.sh/v3/covid-19/countries`)
    .then(response => {
      this.countries = response.data
    })
    .catch(e => {
      this.errors.push(e)
    })

  }}
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family:
    'Quicksand',
    'Source Sans Pro',
    -apple-system,
    BlinkMacSystemFont,
    'Segoe UI',
    Roboto,
    'Helvetica Neue',
    Arial,
    sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
