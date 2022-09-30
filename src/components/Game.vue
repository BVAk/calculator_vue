<template>
  <div>
    <img />
    <img />
  </div>
  <span>The answer is calculation</span>
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
</style>
