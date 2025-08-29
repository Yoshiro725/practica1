<template>
  <div id="app">
    <GenerarRFC />
  </div>
</template>

<script>
import GenerarRFC from './components/GenerarRFC.vue'

export default {
  name: 'App',
  components: {
    GenerarRFC
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
