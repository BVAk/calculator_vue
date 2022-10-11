<template>
  <div id="hangman">
    <span id="top_block" />
    <span id="left_block" />
    <span id="right_block" />
    <span v-if="tries<=3" id="head" />
    <span v-if="tries<=2" id="body" />
    <span v-if="tries<=1" id="right_hand" />
    <span v-if="tries<=1" id="left_hand" />
    <span v-if="tries==0" id="right_leg" />
    <span v-if="tries==0" id="left_leg" />
  </div>
  <span>The answer is calculation</span>
  <div>
    <span class="key" v-for="item in clientValue" :key="item">{{item}}</div>
  </div>
  <div class="buttons" @click="clickNumber" :disable="isDisable">
    <button>0</button>
    <button>1</button>
    <button>2</button>
    <button>3</button>
    <button>4</button>
    <button>5</button>
    <button>6</button>
    <button>7</button>
    <button>8</button>
    <button>9</button>
    <button>.</button>
  </div>
  <div v-if="tries==0">
  <h1>You are lose!</h1> 
  <span> The right answer is {{value}}</span>
  <button id="returnButton" @click="returnCalc">Return to calculator</button>
  </div>
</template>
<script>
export default {
  name: 'Game',
  props: {
    value: Number,
  },
  data() {
    return {
      clientValue: String(this.value).replace(/[0-9]|\./g, '_').split(''),
      secretValue: String(this.value).split(''),
      tries: 4,
      isDisable: false,
    };
  },
  methods: {
    clickNumber(e) {
      if(this.isDisable) return;
      e.target.disabled=true;
      const element = e.target.innerText;
      let idx = this.secretValue.indexOf(element);
      if (idx !== -1) {
        while (idx !== -1) {
          this.clientValue[idx]=element;
          idx = this.secretValue.indexOf(element, idx + 1);
        }
      } else {
        this.tries = this.tries-1;
      }
      if(this.clientValue.join('')==this.value) {
        this.$emit('changeForGame', true, this.value)
      } else if (this.tries==0) this.isDisable=true;
    },
    returnCalc() {
      this.$emit('changeForGame', true, this.value)
    }
  },
};
</script>
<style>
.buttons {
  display: flex;
  justify-content: center;
}
button {
  width: 50px;
  height: 50px;
}
#hangman {
  position: relative;
  width: 200px;
  height: 200px;
  margin: auto;
  padding: 10px;
}

#left_block {
  display: block;
  position: absolute;
  width: 1px;
  height: 200px;
  background-color: black;
}

#top_block {
  display: block;
  position: absolute;
  width: 160px;
  height: 1px;
  background-color: black;
}

#right_block {
  display: block;
  position: absolute;
  width: 1px;
  height: 30px;
  top: 10px;
  right: 50px;
  background-color: black;
}

#head {
  display: block;
  position: absolute;
  width: 30px;
  height: 30px;
  top: 40px;
  right: 35px;
  border-radius: 50%;
  border: 1px solid black;
}

#body {
  display: block;
  position: absolute;
  width: 1px;
  height: 30px;
  top: 71px;
  right: 50px;
  background-color: black;
}

#right_hand {
  display: block;
  position: absolute;
  width: 1px;
  height: 25px;
  top: 67px;
  right: 62px;
  background-color: black;
  transform: rotate(70deg);
}

#left_hand {
  display: block;
  position: absolute;
  width: 1px;
  height: 25px;
  top: 67px;
  right: 38px;
  background-color: black;
  transform: rotate(-70deg);
}

#right_leg {
  display: block;
  position: absolute;
  width: 1px;
  height: 25px;
  top: 99px;
  right: 57px;
  background-color: black;
  transform: rotate(32deg);
}

#left_leg {
  display: block;
  position: absolute;
  width: 1px;
  height: 25px;
  top: 99px;
  right: 43px;
  background-color: black;
  transform: rotate(-32deg);
}

.key {
  padding: 5px 10px;
}

#returnButton {
  margin: 10px auto;
  padding: 10px;
  height: auto;
  width: auto;
  background-color: #9599e2;
  color: white;
}
</style>
