<template>
  <div id="app">
    <AirPollution />
  </div>
</template>

<script>
import AirPollution from "@/components/WeatherAppApi.vue";


export default {
  name: "App",
  components: {
    AirPollution,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
