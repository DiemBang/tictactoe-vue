<script setup lang="ts">
import { ref } from "vue";
import Square from "./Square.vue"
import GameStatus from "./GameStatus.vue"

const props = defineProps({
  player1: String,
  player2: String,
});

const board = ref<(string | null)[]>(Array(9).fill(null));
const currentPlayer = ref("X");
const status = ref<string>(`Player ${props.player1}'s turn` );
const gameOver = ref<boolean>(false);


const player1Score = ref(0);
const player2Score = ref(0);

const player1Symbol = ref('X');



const handleSquareClick = (index: number) => {
  if (!gameOver.value && board.value[index] === null) {
    board.value[index] = currentPlayer.value;
    checkForWinner();
    if (!gameOver.value) {
      currentPlayer.value = currentPlayer.value === "X" ? "O" : "X";
      status.value = `Player ${currentPlayer.value === 'X' ? props.player1 : props.player2}'s turn`;
    }
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
      gameOver.value = true;
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
    gameOver.value = true;
    status.value = "It's a draw!";
  }
};

</script>

<template>
  <div id="gameBoard">
    <GameStatus :status="status" />
    
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
