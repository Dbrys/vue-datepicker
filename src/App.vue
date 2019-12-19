<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <datePicker/>
  </div>
</template>

<script>
import datePicker from './components/DatepickerInput.vue'

export default {
  name: 'app',
  components: {
    datePicker
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
