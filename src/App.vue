<template>
  <div id="app">
    <Transport v-on:avgAmptoApp="ampReceive"/>
    <Graphics/>
  </div>
</template>

<script>

import Transport from './components/Transport.vue'
import Graphics from './components/Graphics.vue'

export default {
  data () {
    return {
      avgAmp: {
        type: Number,
        default: 0
      }
    }
  },
  name: 'app',
  components: {
    Transport,
    Graphics
  },
  methods: {
    ampReceive(value) {
      this.avgAmp = value
      console.log(value)
    }
  }
}
</script>

<style>
#app {
  background-color: #2c3e50;
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
