<template>
  <div id="calc">
    <div class="calcRow">
      <span id="field">{{ convertedValue }}</span>
      <button class="button" id="clear" @click="clear">Clear</button>
    </div>
    <div class="calcRow">
      <button class="button" @click="calculation">7</button>
      <button class="button" @click="calculation">8</button>
      <button class="button" @click="calculation">9</button>
      <button class="funcs" @click="calculation">/</button>
    </div>
    <div class="calcRow">
      <button class="button" @click="calculation">4</button>
      <button class="button" @click="calculation">5</button>
      <button class="button" @click="calculation">6</button>
      <button class="funcs" @click="calculation">*</button>
    </div>
    <div class="calcRow">
      <button class="button" @click="calculation">1</button>
      <button class="button" @click="calculation">2</button>
      <button class="button" @click="calculation">3</button>
      <button class="funcs" @click="calculation">+</button>
    </div>
    <div class="calcRow">
      <button class="button" :disabled="disablepoint" @click="calculation">
        .
      </button>
      <button class="button" @click="calculation">0</button>
      <button class="funcs" @click="calculate">=</button>
      <button class="funcs" @click="calculation">-</button>
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
      disablepoint: false,
      value: this.valueComplete,
    };
  },
  methods: {
    clear() {
      this.value = '';
    },
    calculation(event) {
      const funcSymbol = ['/', '+', '-', '*'];
      const e = event.target.innerHTML;
      if (String(this.value) === '0') {
        if (e !== ' . ') {
          return (this.value = e);
        } else this.disablepoint = true;
      } else if (e === ' . ') {
        this.disablepoint = true;
        if (funcSymbol.includes(this.value.slice(-1))) {
          return (this.value += `0${e}`);
        }
      }
      if (event.target.classList[0].includes('funcs')) {
        this.disablepoint = false;
        if (funcSymbol.includes(this.value.slice(-1))) {
          return (this.value =
            this.value.substring(0, this.value.length - 1) + e);
        }
      }
      return (this.value += e);
    },
    calculate() {
      this.value = evaluate(this.value.replaceAll(' ', ''));
      if (String(this.value).includes('.'))
        this.value = parseFloat(this.value).toFixed(2);
      this.$emit('changeForGame', false, this.value);
    },
  },
  computed: {
    convertedValue() {
      return String(this.value).replaceAll(' ', '');
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
  border: 2px solid black;
  border-radius: 10px;
  box-shadow: 0 10px 10px -5px;
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
}

.button {
  background-color: #ffffff;
  border: 0;
  border-radius: 16px;
  box-sizing: border-box;
  color: #111827;
  font-family: 'Inter var', ui-sans-serif, system-ui, -apple-system, system-ui,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, 'Noto Sans', sans-serif,
    'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol', 'Noto Color Emoji';
  font-size: 0.875rem;
  font-weight: 600;
  line-height: 1.25rem;
  padding: 0.75rem 1rem;
  text-align: center;
  text-decoration: none #d1d5db solid;
  text-decoration-thickness: auto;
  box-shadow: 0 1px 3px 0 rgb(0 0 0 / 20%), 0 1px 2px 0 rgb(0 0 0 / 10%);
  cursor: pointer;
  user-select: none;
  -webkit-user-select: none;
  touch-action: manipulation;
}

.button:hover {
  background-color: rgb(249, 250, 251);
}

.button:focus {
  outline: 2px solid transparent;
  outline-offset: 2px;
}

.button:focus-visible {
  box-shadow: none;
}

.funcs {
  background-color: #1899d6;
  color: #ffffff;
  appearance: button;
  background-color: #1899d6;
  border: solid transparent;
  border-radius: 16px;
  border-width: 0 0 4px;
  box-sizing: border-box;
  cursor: pointer;
  display: inline-block;
  font-family: din-round, sans-serif;
  font-size: 15px;
  font-weight: 700;
  letter-spacing: 0.8px;
  margin: 0;
  outline: none;
  overflow: visible;
  text-align: center;
  text-transform: uppercase;
  touch-action: manipulation;
  transform: translateZ(0);
  transition: filter 0.2s;
  user-select: none;
  -webkit-user-select: none;
  vertical-align: middle;
  white-space: nowrap;
}

.funcs:after {
  background-clip: padding-box;
  background-color: #1cb0f6;
  border: solid transparent;
  border-radius: 16px;
  border-width: 0 0 2px;
  bottom: -4px;
  content: '';
  left: 0;
  position: absolute;
  right: 0;
  top: 0;
  z-index: -1;
}

.button:main,
.button:focus {
  user-select: auto;
}

#clear {
  height: 40px;
  width: 90px;
}

.funcs:hover:not(:disabled) {
  filter: brightness(1.1);
  -webkit-filter: brightness(1.1);
}

.funcs:disabled {
  cursor: auto;
}
</style>
