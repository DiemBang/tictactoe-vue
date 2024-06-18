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

const addScore = (index: number) => {};

const checkForWinner = () => {
  const winningCombinations = [
    [0, 1, 2],
    [3, 4, 5],
    [6, 7, 8],
    [0, 3, 6],
    [1, 4, 7],
    [2, 5, 8],
    [0, 4, 8],
    [2, 4, 6],
  ];
  for (const combination of winningCombinations) {
    const [a, b, c] = combination;
    if (
      board.value[a] &&
      board.value[a] === board.value[b] &&
      board.value[a] === board.value[c]
    ) {
      if (board.value[a] === player1Symbol.value) {
        status.value = `${props.player1} wins!`;
      } else {
        status.value = `${props.player2} wins!`;
      }

      // To-do: add players score
      addScore(a);
      return;
    }
  }
  if (!board.value.includes(null)) {
    status.value = "It's a draw!";
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
