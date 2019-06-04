<template>
  <div class="app">
    <div>
      <h1>Synonym Machine</h1>
      <input type="text" placeholder="Enter any ol' word">
      <button class="submit-button" v-on:click="handleSubmit">Let's find them!</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "app",
  methods: {
    handleSubmit: function() {
      alert("Works?");
    }
  }
};
</script>

<style>
.app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
