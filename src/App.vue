<template>
  <div id="app">
    <TimeSheetCheck/>
  </div>
</template>

<script>
import TimeSheetCheck from './views/TimeSheetCheck.vue'

export default {
  name: 'App',
  components: {
    TimeSheetCheck
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
