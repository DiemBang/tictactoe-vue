<script setup lang="ts">
import { ref } from "vue";
import Square from "./Square.vue";
import GameStatus from "./GameStatus.vue";
import JoinGamePage from "./JoinGamePage.vue";
import ScoreBoard from "./ScoreBoard.vue";

const gamePhase = ref<"setup" | "play">("setup");

const board = ref<(string | null)[]>(Array(9).fill(null));
const currentPlayer = ref("X");

const gameOver = ref<boolean>(false);

const player1 = ref<string | null>(null);
const player2 = ref<string | null>(null);
const status = ref<string>(`Player ${player1.value}'s turn`);

const player1Score = ref(0);
const player2Score = ref(0);

const player1Symbol = ref("X");

const startGame = (player1Name: string, player2Name: string) => {
  gamePhase.value = "play";
  localStorage.setItem("player1", player1Name);
  localStorage.setItem("player2", player2Name);
  status.value = `Player ${player1Name}'s turn`;
  console.log("starting game");
  player1.value = player1Name;
  player2.value = player2Name;
};

const handleSquareClick = (index: number) => {
  if (!gameOver.value && board.value[index] === null) {
    board.value[index] = currentPlayer.value;
    checkForWinner();
    if (!gameOver.value) {
      currentPlayer.value = currentPlayer.value === "X" ? "O" : "X";
      status.value = `Player ${
        currentPlayer.value === "X" ? player1.value : player2.value
      }'s turn`;
    }
    console.log(player1.value);
  }
};

const addScore = (winnerSymbol: string) => {
  if (winnerSymbol === player1Symbol.value) {
    player1Score.value++;
  } else {
    player2Score.value++;
  }
};

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
        status.value = `${player1.value} wins!`;
      } else {
        status.value = `${player2.value} wins!`;
      }

      // Add players score
      addScore(board.value[a]);
      return;
    }
  }
  if (!board.value.includes(null)) {
    gameOver.value = true;
    status.value = "It's a draw!";
  }
};

const resetGame = () => {
  board.value = Array(9).fill(null);
  currentPlayer.value = "X";
  status.value = `Player ${player1.value}'s turn`;
  gameOver.value = false;
};

const resetToInitialState = () => {
  gamePhase.value = "setup";
  localStorage.removeItem("player1");
  localStorage.removeItem("player2");
  resetGame();
};
</script>

<template>
  <div id="gameContainer">
    <div v-if="gamePhase === 'setup'">
      <JoinGamePage @joinGame="startGame" />
    </div>
    <div v-else>
      <ScoreBoard :player1="player1" :player2="player2" :player1Score="player1Score" :player2Score="player2Score" />
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
        <div>
          <p><button @click="resetGame">Reset Game</button></p>
          <p><button @click="resetToInitialState">Restart Game</button></p>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.board {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
}
</style>
