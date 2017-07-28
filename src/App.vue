<template>
  <div id="app">
    <v-for-render></v-for-render>
  </div>
</template>

<script>
import VForRender from './components/VForRender'

export default {
  name: 'app',
  components: {
    VForRender
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: left;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
