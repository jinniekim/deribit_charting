<template>
  <div id="app">
    <DeribitChart/>
  </div>
</template>

<script>
import DeribitChart from './components/DeribitChart.vue'

export default {
  name: 'App',
  components: {
    DeribitChart
  }
}
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
