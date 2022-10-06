<template>
  <div id="app">
    <Calculator
      v-if="showCalculator"
      v-bind:value="value"
      @changeForGame="changeForGame"
    />
    <Game v-else v-bind:value="value" @changeForGame="changeForGame" />
    <!-- <Game :value="10" /> -->
  </div>
</template>

<script>
import Calculator from './components/Calculator.vue';
import Game from './components/Game.vue';

export default {
  name: 'App',
  data() {
    return {
      showCalculator: true,
      value: 0,
    };
  },
  components: {
    Calculator,
    Game,
  },
  methods: {
    changeForGame(status, value) {
      console.log(value);
      this.value = value;
      this.showCalculator = status;
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
</style>
