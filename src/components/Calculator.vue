<template>
  <div id="calc">
    <div class="calcRow">
      <span id="field" @add="(i) => count += i"></span>
    </div>
    <div class="calcRow">
      <Button value="7"></Button>
      <Button value="8"></Button>
      <Button value="9"></Button>
      <Button value="/"></Button>
    </div>
    <div class="calcRow">
      <Button value="4"></Button>
      <Button value="5"></Button>
      <Button value="6"></Button>
      <Button value="*"></Button>
    </div>
    <div class="calcRow">
      <Button value="1"></Button>
      <Button value="2"></Button>
      <Button value="3"></Button>
      <Button value="+"></Button>
    </div>
    <div class="calcRow">
      <Button value="0"></Button>
      <Button value="."></Button>
      <Button value="="></Button>
      <Button value="-"></Button>
    </div>
  </div>
</template>

<script>
import Button from './Button.vue';

export default {
  name: 'Calculator',
  components: { Button },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#calc {
  height: auto;
  width: fit-content;
  margin: auto;
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
  width: 100%;
  margin: 5px;
  height: 40px;
  background-color: white;
  border-radius: 10px;
}
</style>
