<template>
  <div id="app">
    <Transport/>
    <Graphics/>
  </div>
</template>

<script>

import Transport from './components/Transport.vue'
import Graphics from './components/Graphics.vue'

export default {
  name: 'app',
  components: {
    Transport,
    Graphics
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
