
<template>
  <div id="app">
    
    <TextFormatter />
    <ContactInfo></ContactInfo>
  </div>
</template>

<script>
import TextFormatter from './components/TextFormatter.vue'
import ContactInfo from './components/ContactInfo.vue';



export default {
  name: 'App',
  components: {
    TextFormatter,
    ContactInfo
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