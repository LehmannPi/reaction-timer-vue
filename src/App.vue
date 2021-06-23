
// * Create boolean for game status (on/off) [x]
// * Create timer - counting randomly between 2 and 7 sec [x]
// * Show the block that will be shown in the screen [x]
// * Tie the block appearance to the status isPlaying [x]
// * Disable button while game is currently going on [x]
// * Receive emission of Block component end handle it's variable in a function [x]
// * 

<template>
  <h1>Reaction Timer</h1>
  <p>Click on the big button as soon as it appears</p>
  <p class="br">(Clique no botão grande logo que ele aparecer)</p>
  <button @click="start" :disabled="isPlaying">Play</button>
  <Block v-if="isPlaying" v-bind:delay="delay" @end="endGame" />
  <Results v-if="showResults" :score="score" />
  
</template>

<script>
import Block from "./components/Block.vue";
import Results from "./components/Results.vue";

export default {
  name: "App",
  components: { Block, Results },
  data() {
    return {
      isPlaying: false,
      delay: null, // will be set after
      score: null,
      showResults: false,
      // showScore: false,
    };
  },
  methods: {
    start() {
      this.delay = 2000 + Math.random() * 5000;
      this.isPlaying = true;
      this.showResults = false;
      // console.log(this.delay);
    },
    endGame(reacTime) {
      this.score = reacTime;
      this.isPlaying = false;
      this.showResults = true;
    },
  },
};
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
.br {
  font-size: 0.9em;
  font-style: italic;
  margin: 16px;
}
button {
  background: #0faf87;
  color: white;
  border: none;
  padding: 8px 16px;
  border-radius: 4px;
  font-size: 16px;
  letter-spacing: 1px;
  cursor: pointer;
  margin: 10px;
}
button[disabled] {
  opacity: 0.2;
  cursor: not-allowed;
}
</style>
