<script setup lang="ts">
import { ref } from "vue";

const clickedSquare = () => {};

let square = ref<number[]>([]);
for (let i = 0; i <= 9; i++) square.value.push(null);
</script>

<template>
  <div id="board">
    <div class="square" v-for="(value, index) in 9" :key="index">
        {{ square.value[index] }} 
    </div>
  </div>
</template>

<style scoped>
#board {
  height: 400px;
  width: 400px;
  margin: 0 auto;
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
}

.square {
  width: 30%;
  background-color: lightpink;
  border: 1px solid black;
}
</style>
