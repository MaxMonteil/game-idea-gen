<template>
  <div id="app">
    <the-generator />
    <the-about />
    <the-footer />
  </div>
</template>

<script>
import TheGenerator from './components/TheGenerator.vue'
import TheAbout from './components/TheAbout.vue'
import TheFooter from './components/TheFooter.vue'

export default {
  name: 'app',
  components: {
    TheGenerator,
    TheAbout,
    TheFooter
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
  color: #ED9B40;
  background-color: #FFEEDB;
  user-select: none;
}
</style>
