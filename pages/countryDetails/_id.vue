<template>
  <div>
    <h1 class="title">Tracking Coronavirus (COVID-19) for</h1>

    <v-btn small v-on:click="getTodayData">Today</v-btn>
    <v-btn small v-on:click="getYesterdayData">Yesterday</v-btn>
    <v-btn small v-on:click="getTwoDaysAgoData">Before 2 days</v-btn>
    <v-data-table
      :headers="headers"
      :items="[countrieDeatils]"
      :items-per-page="1"
      @click:row="handleClick"
      class="elevation-1"
    ></v-data-table>
  </div>
</template>

<script>
const axios = require("axios");
const $router = require("vue-router");
import dashboardCard from "../../components/dashboard/dashboard-card";
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
      countrieDeatils: {}
    };
  },
  components: {
    dashboardCard: dashboardCard
  },
  methods: {
    getYesterdayData: function() {
      axios
        .get(
          `https://disease.sh/v3/covid-19/countries/Afghanistan?strict=true?yesterday=true`
        )
        .then(response => {
          this.countrieDeatils = response.data;
        })
        .catch(e => {
          this.errors.push(e);
        });
    },
    getTwoDaysAgoData: function() {
      axios
        .get(
          `https://disease.sh/v3/covid-19/countries/Afghanistan?strict=true?twoDaysAgo=true`
        )
        .then(response => {
          this.countrieDeatils = response.data;
        })
        .catch(e => {
          this.errors.push(e);
        });
    },
    getTodayData: function() {
      axios
        .get(`https://disease.sh/v3/covid-19/countries/Afghanistan?strict=true`)
        .then(response => {
          this.countrieDeatils = response.data;
        })
        .catch(e => {
          this.errors.push(e);
        });
    },
    handleClick: function(value) {
      console.log(value);
    }
  },
  created() {
    this.getTodayData();
  }
};
</script>

<style>
.title {
  display: flex;
  justify-content: center;
}
</style>
