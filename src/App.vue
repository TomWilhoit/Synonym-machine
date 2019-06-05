<template>
  <div class="app">
    <div>
      <h1>Synonym Machine</h1>
      <input type="text" placeholder="Enter any ol' word">
      <button class="submitButton" v-on:click="handleSubmit">Let's find them!</button>
    </div>
    <div class="synonym-container">
      <h2 class="synonyms-list"></h2>
      <h3></h3>
      <div></div>
    </div>
  </div>
</template>
<script>
import apiKey from "../apiKey.js";
export default {
  name: "app",
  methods: {
    handleSubmit: async function(e) {
      let word =
        e.target.parentElement.parentElement.children[0].children[1].value;
      if (word) {
        const response = await this.fetchSynonyms(word);
        const data = await response.json();
        const synonyms = [];
        data[0].meta.syns[0].forEach(syn => {
          synonyms.push(syn);
        });
        e.target.parentElement.parentElement.children[1].children[0].innerText = word;
        e.target.parentElement.parentElement.children[1].children[1].innerText =
          data[0].shortdef[0];
        let newButtons = synonyms.map(syn => {
          return `<button ref="syn-button" value=${syn} class="syn-button">${syn}</button>`;
        });
        e.target.parentElement.parentElement.children[1].children[2].innerHTML = newButtons;
        let clicks = this.$el.querySelectorAll(".syn-button");
        clicks.forEach(button =>
          button.addEventListener("click", () => this.check(e, button.value))
        );
      } else {
        e.target.parentElement.parentElement.children[1].children[0].innerText = `You have to enter a word, chucklehead`;
      }
    },
    fetchSynonyms: async function(word) {
      let url = `https://www.dictionaryapi.com/api/v3/references/thesaurus/json/${word}?key=${apiKey}`;
      return await fetch(url);
    },
    check: async function(e, value) {
      const response = await this.fetchSynonyms(value);
      const data = await response.json();
      const shortdef = data[0].shortdef;
      const synonyms = data[0].meta.syns[0];
      e.srcElement.parentElement.parentElement.children[1].children[0].innerText = value;
      e.srcElement.parentElement.parentElement.children[1].children[1].innerText = shortdef;
      let newButtons = synonyms.map(syn => {
        return `<button ref="syn-button" value=${syn} class="syn-button">${syn}</button>`;
      });
      e.srcElement.parentElement.parentElement.children[1].children[2].innerHTML = newButtons;
      let clicks = this.$el.querySelectorAll(".syn-button");
      clicks.forEach(button =>
        button.addEventListener("click", () => this.check(e, button.value))
      );
    }
  }
};
</script>

<style>
body {
  color: azure;
  width: 100%;
  height: 100%;
  background-color: #2c3e50;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  color: #2c3e50;
  margin-top: 60px;
  background-color: #2c3e50;
  color: azure;
}

.synonym-container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  margin: 25px;
}

.syn-button {
  height: 30px;
  font-size: 20px;
  background-color: steelblue;
  color: white;
  font-style: italic;
  margin: 10px;
  max-width: 80%;
}

.submitButton {
  height: 26px;
}
</style>
