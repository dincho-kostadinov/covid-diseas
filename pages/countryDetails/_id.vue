<template>
  <v-container class="grey lighten-5">
    <v-row>
      <v-col>
        <h1 class="title">
          Tracking Coronavirus (COVID-19) for {{ this.$route.params.id }}
        </h1>
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
          :items="[countrieDeatils]"
          :items-per-page="1"
          @click:row="handleClick"
          class="elevation-1"
        ></v-data-table>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
const axios = require("axios");

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
        { text: "Active Cases", value: "active" },
        { text: "One test per people", value: "oneTestPerPeople" },
        { text: "Recovered per One Million", value: "recoveredPerOneMillion" },
        { text: "Tests", value: "tests" }
      ],
      countrieDeatils: {}
    };
  },
  components: {},
  methods: {
    getData: function(filter) {
      var url = "";
      if (filter) {
        this.url = `https://disease.sh/v3/covid-19/countries/${this.$route.params.id}?${filter}=true&strict=true`;
      } else {
        this.url = `https://disease.sh/v3/covid-19/countries/${this.$route.params.id}?strict=true`;
      }
      axios
        .get(this.url)
        .then(response => {
          this.countrieDeatils = response.data;
        })
        .catch(e => {
          this.errors.push(e);
        });
    }
  },
  created() {
    this.getData();
  }
};
</script>

<style>
.title {
  display: flex;
  justify-content: center;
}
</style>
