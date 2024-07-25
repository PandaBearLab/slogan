
<template>
  <div id="app">
    <h1 >大字报</h1>
    <TextFormatter />
  </div>
</template>

<script>
import TextFormatter from './components/TextFormatter.vue'

export default {
  name: 'App',
  components: {
    TextFormatter
  }
}
</script>

<style>
#app {
  font-family: 'Huiwen Mingchao', Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>