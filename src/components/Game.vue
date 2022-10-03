<template>
  <div id="hangman">
    <span id="top_block" />
    <span id="left_block" />
    <span id="right_block" />
    <span id="head" />
    <span id="body" />
    <span id="right_hand" />
    <span id="left_hand" />
    <span id="right_leg" />
    <spn id="left_leg" />
  </div>
  <span>The answer is calculation</span>
  <div>
    <span v-for="item in String(value).length" :key="item">_</div>
  </div>
  <div class="buttons">
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
</template>
<script>
export default {
  name: 'Game',
  data() {
    return {};
  },
  props: {
    value: Number,
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
  width: 150px;
  height: 1px;
  background-color: black;
}

#right_block {
  display: block;
  position: absolute;
  width: 1px;
  height: 40px;
  top: 0;
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
</style>
