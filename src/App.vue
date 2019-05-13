<template>
  <div id="app">
    <TheGenerator />
  </div>
</template>

<script>
import TheGenerator from './components/TheGenerator.vue'

export default {
  name: 'app',
  components: {
    TheGenerator
  }
}
</script>

<style>
body {
  margin: 0;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  padding: 16px;
  color: #ED9B40;
  background-color: #FFEEDB;
  user-select: none;
}
</style>
