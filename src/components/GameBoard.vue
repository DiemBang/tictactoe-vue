<script setup lang="ts">
import { ref } from "vue";
import Square from "./Square.vue"


const board = ref<(string | null)[]>(Array(9).fill(null));
const currentPlayer = ref("X");
const status = ref("Player X's turn");

const props = defineProps({
  player1: String,
  player2: String,
});

const handleSquareClick = (index: number) => {
  if (board.value[index] === null) {
    board.value[index] = currentPlayer.value;
    currentPlayer.value = currentPlayer.value === "X" ? "O" : "X";
    status.value = `Player ${currentPlayer.value}'s turn`;
    
    console.log(props.player1);
  }
};




</script>

<template>
  <div id="gameBoard">
    
    <div class="board">
      <Square
        v-for="(value, index) in board"
        :key="index"
        :value="value"
        @click="handleSquareClick(index)"
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
