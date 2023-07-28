<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <h2>Welcome to my weather app</h2>

    <weather-display></weather-display>

  </div>
</template>

<script>
import WeatherDisplay from './components/WeatherDisplay.vue'


export default {
  name: 'App',
  components: {
    WeatherDisplay
    
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
