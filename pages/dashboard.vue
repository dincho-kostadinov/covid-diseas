<template>
  <v-container class="grey lighten-5">
    <v-row>
      <v-col>
        <h1 class="title">Tracking Coronavirus (COVID-19)</h1>
      </v-col>
    </v-row>
    <v-row>
      <v-col>
        <dashboardCard
          title="Confirmed"
          :results="CardData.cases"
        ></dashboardCard>
      </v-col>
      <v-col>
        <dashboardCard
          title="Recovered"
          :results="CardData.recovered"
        ></dashboardCard>
      </v-col>
      <v-col>
        <dashboardCard
          title="Deaths"
          :results="CardData.deaths"
        ></dashboardCard>
      </v-col>
      <v-col>
        <dashboardCard
          title="Active"
          :results="CardData.active"
        ></dashboardCard>
      </v-col>
    </v-row>
    <v-row>
      <v-col>
        <v-btn small v-on:click="getData">Today</v-btn>
        <v-btn small v-on:click="getData('yesterday')">Yesterday</v-btn>
        <v-btn small v-on:click="getData('twoDaysAgo')">Before 2 days</v-btn>
      </v-col>
    </v-row>
    <v-row>
      <v-col>
        <v-data-table
          :headers="headers"
          :items="countries"
          :items-per-page="15"
          @click:row="handleClick"
          class="elevation-1"
        ></v-data-table>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
const axios = require("axios");
const $router = require("vue-router");
import dashboardCard from "../components/dashboard/dashboard-card.vue";
export default {
  data() {
    return {
      headers: [
        {
          text: "Country",
          align: "start",
          sortable: false,
          value: "country"
        },
        { text: "Total cases", value: "cases" },
        { text: "New Cases", value: "todayCases" },
        { text: "Total Deaths", value: "deaths" },
        { text: "New Deaths", value: "todayDeaths" },
        { text: "Total Recovered", value: "recovered" },
        { text: "Active Cases", value: "active" }
      ],
      countries: [],
      CardData: {}
    };
  },
  components: {
    dashboardCard: dashboardCard
  },
  methods: {
    getData: function(filter) {
      var url = "";
      if (filter) {
        this.url = `https://disease.sh/v3/covid-19/countries?${filter}=true`;
      } else {
        this.url = `https://disease.sh/v3/covid-19/countries`;
      }
      axios
        .get(this.url)
        .then(response => {
          this.countries = response.data;
        })
        .catch(e => {
          this.errors.push(e);
        });
    },
    handleClick: function(value) {
      this.$router.push({ path: `/countryDetails/${value.country}` });
    }
  },
  created() {
    this.getData();

    axios
      .get(`https://disease.sh/v3/covid-19/all`)
      .then(response => {
        this.CardData = response.data;
      })
      .catch(e => {
        this.errors.push(e);
      });
  }
};
</script>

<style>
.title {
  display: flex;
  justify-content: center;
}
</style>
