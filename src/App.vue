<template>
  <div id="app">
    <Transport msg="Press Start to Hear Synth Music"/>
  </div>
</template>

<script>

import Transport from './components/Transport.vue'

export default {
  name: 'app',
  components: {
    Transport
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
