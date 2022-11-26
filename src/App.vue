<template>
  <div id="app">
    <hello></hello>
    <!-- <radial-chart/> -->
  </div>
</template>

<script>
import Hello from "./components/Hello";
import RadialChartVue from "./views/RadialChart.vue";
export default {
  name: "app",
  components: {
    Hello,
    'radial-chart' : RadialChartVue
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

#app .logo {
  text-align: center;
}
</style>
