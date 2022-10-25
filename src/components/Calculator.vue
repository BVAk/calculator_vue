<template>
  <div id="calc">
    <div class="calcRow">
      <span id="field">{{ value }}</span>
      <button id="clear" @click="clear">Clear</button>
    </div>
    <div class="calcRow">
      <button @click="calculation('7')">7</button>
      <button @click="calculation('8')">8</button>
      <button @click="calculation('9')">9</button>
      <button @click="calculation('/')">/</button>
    </div>
    <div class="calcRow">
      <button @click="calculation('4')">4</button>
      <button @click="calculation('5')">5</button>
      <button @click="calculation('6')">6</button>
      <button @click="calculation('*')">*</button>
    </div>
    <div class="calcRow">
      <button @click="calculation('1')">1</button>
      <button @click="calculation('2')">2</button>
      <button @click="calculation('3')">3</button>
      <button @click="calculation('+')">+</button>
    </div>
    <div class="calcRow">
      <button @click="calculation('0')">0</button>
      <button @click="calculation('.')">.</button>
      <button @click="calculate">=</button>
      <button @click="calculation('-')">-</button>
    </div>
  </div>
</template>
<script>
import { evaluate } from 'mathjs';
export default {
  name: 'Calculator',

  props: {
    valueComplete: {
      Type: String,
      default: '',
    },
  },
  data() {
    return {
      value: this.valueComplete,
    };
  },
  methods: {
    clear() {
      this.value = '';
    },
    calculation(e) {
      this.value += e;
    },
    calculate() {
      this.value = evaluate(this.value);
      if (String(this.value).includes('.'))
        this.value = parseFloat(this.value).toFixed(2);
      this.$emit('changeForGame', false, this.value);
    },
  },
};
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@font-face {
  font-family: 'Orbitron';
  font-style: normal;
  font-weight: 400 900;
  font-display: block;
  src: url(https://fonts.gstatic.com/s/orbitron/v25/yMJRMIlzdpvBhQQL_Qq7dy1biN15.woff2)
    format('woff2');
  unicode-range: U+0000-00FF, U+0131, U+0152-0153, U+02BB-02BC, U+02C6, U+02DA,
    U+02DC, U+2000-206F, U+2074, U+20AC, U+2122, U+2191, U+2193, U+2212, U+2215,
    U+FEFF, U+FFFD;
}

#calc {
  height: auto;
  width: 330px;
  margin: auto;
  padding: 5px;
  background-color: #8bc6ec;
  background-image: linear-gradient(135deg, #8bc6ec 0%, #9599e2 100%);
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  align-items: center;
}

.calcRow {
  display: flex;
  flex-direction: row;
  justify-content: space-around;
  align-items: center;
  width: 100%;
}

#field {
  display: flex;
  justify-content: end;
  align-items: center;
  max-width: 227px;
  width: 100%;
  height: 40px;
  overflow: hidden;
  margin: 5px;
  padding-right: 5px;
  background-color: white;
  border-radius: 10px;
  font-optical-sizing: auto;
  font-weight: 500;
  font-size: 25px;
  font-style: normal;
  font-stretch: normal;
  line-height: initial;
  font-family: 'Orbitron', sans-serif;
}

button {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 70px;
  width: 70px;
  margin: 5px;
  border-radius: 10px;
  border: 1px solid;
}

#clear {
  height: 40px;
  width: 90px;
}
</style>
