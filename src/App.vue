<template>
  <div id="app">
    <Calculator
      v-if="showCalculator"
      v-bind:valueComplete="value"
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
      this.value = value;
      this.showCalculator = status;
    },
  },
};
</script>

<style>
@font-face {
  font-family: 'digital';
  font-style: normal;
  font-weight: normal;
  src: url('public/font.eot'); /* IE9 Compat Modes */
  src: url('public/font.eot?#iefix') format('embedded-opentype'),
    /* IE6-IE8 */ url('public/font.woff2') format('woff2'),
    /* Super Modern Browsers */ url('public/font.woff') format('woff'),
    /* Pretty Modern Browsers */ url('public/font.ttf') format('truetype'),
    /* Safari, Android, iOS */ url('public/font.svg#svgFontName') format('svg'); /* Legacy iOS */
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
