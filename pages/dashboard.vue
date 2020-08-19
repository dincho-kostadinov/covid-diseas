<template>
  <div>
    <h1 class="title">Tracking Coronavirus (COVID-19)</h1>

    <dashboardCard title="Confirmed" :results="CardData.cases"></dashboardCard>
    <dashboardCard
      title="Recovered"
      :results="CardData.recovered"
    ></dashboardCard>
    <dashboardCard title="Deaths" :results="CardData.deaths"></dashboardCard>
    <dashboardCard title="Active" :results="CardData.active"></dashboardCard>
    <v-btn small v-on:click="getTodayData">Today</v-btn>
    <v-btn small v-on:click="getYesterdayData">Yesterday</v-btn>
    <v-btn small v-on:click="getTwoDaysAgoData">Before 2 days</v-btn>
    <v-data-table
      :headers="headers"
      :items="countries"
      :items-per-page="15"
      class="elevation-1"
    ></v-data-table>
  </div>
</template>

<script>
const axios = require("axios");
import dashboardCard from "../components/dashboard/dashboard-card.vue";
export default {
  data() {
    return {
      headers: [
        {
          text: "Id",
          align: "start",
          sortable: false,
          value: "countryInfo._id"
        },
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
    getYesterdayData: function() {
      axios
        .get(`https://disease.sh/v3/covid-19/countries?yesterday=true`)
        .then(response => {
          this.countries = response.data;
        })
        .catch(e => {
          this.errors.push(e);
        });
    },
    getTwoDaysAgoData: function() {
      axios
        .get(`https://disease.sh/v3/covid-19/countries?twoDaysAgo=true`)
        .then(response => {
          this.countries = response.data;
        })
        .catch(e => {
          this.errors.push(e);
        });
    },
    getTodayData: function() {
      axios
        .get(`https://disease.sh/v3/covid-19/countries`)
        .then(response => {
          this.countries = response.data;
        })
        .catch(e => {
          this.errors.push(e);
        });
    }
  },
  created() {
    this.getTodayData();

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
