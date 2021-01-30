<template>
  <div id="app">
    <div id="vis"></div>
  </div>
</template>

<script>
import embed from "vega-embed";
export default {
  name: "App",
  data() {
    return {
      visRef: null,
      worldDataCatByCountry:
        "https://opendata.ecdc.europa.eu/covid19/casedistribution/json/",
      worldDataCatByWeek:
        "https://opendata.ecdc.europa.eu/covid19/nationalcasedeath/json/",
    };
  },
  mounted() {
    this.renderWorldDataCatByCountry();
  },
  renderWorldDataCatByCountry() {
    fetch(this.worldDataCatByCountry).then((res) => {
      res.json().then((data) => {
        console.log(data);
        const opt = {
          $schema: "https://vega.github.io/schema/vega-lite/v4.json",
          description: "A simple bar chart with embedded data.",
          data: {
            values: data,
          },
          mark: "bar",
          encoding: {
            x: { field: "a", type: "ordinal" },
            y: { field: "b", type: "quantitative" },
          },
        };
        embed("#vis", opt);
      });
    });
  },
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
