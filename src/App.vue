<template>
  <div id="app">
    <Myapp />
  </div>
</template>

<script>
import Myapp from './components/Myapp.vue'

export default {
  name: 'app',
  components: {
    Myapp
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


