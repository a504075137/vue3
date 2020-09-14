<template>
  <div>hello {{num}}</div>
  <button @click="add">add</button>
</template>

<script>
import { ref } from "vue";
export default {
  setup() {
    const num = ref(0);
    function add() {
      num.value += 1;
    }
    return { num, add };
  },
};
</script>

<style scoped>
</style>
