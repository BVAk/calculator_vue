<template>
  <div class="button" @click="clickValue">{{ value }}</div>
</template>
<script>
export default {
  name: 'Button',
  props: {
    value: String,
  },
  methods: {
    clickValue() {
      console.log(this.value);
      this.$emit('add', Math.random());
      // this.$emit('update:calculation', this.value);
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.button {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 70px;
  width: 70px;
  margin: 5px;
  border-radius: 10px;
  border: 1px solid;
}
</style>
