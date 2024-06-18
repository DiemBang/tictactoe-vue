<script setup lang="ts">
import { ref } from "vue";
import Square from "./Square.vue"


const board = ref<(string | null)[]>(Array(9).fill(null));




</script>

<template>
  <div id="gameBoard">
    
    <div class="board">
      <Square
        v-for="(value, index) in board"
        :key="index"
        :value="value"
        
      />
    </div>
  </div>
</template>

<style scoped>
.board {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
}
</style>
