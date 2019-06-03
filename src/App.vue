<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <Synonyms msg="Check 1 2"/>
  </div>
</template>

<script>
import Synonyms from './components/Synonyms.vue'



export default {
  methods: {
  
},
  name: 'app',
  components: {
    Synonyms
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
