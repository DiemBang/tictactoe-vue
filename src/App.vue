<script setup lang="ts">
import { ref } from "vue";
import GameBoard from "./components/GameBoard.vue";
import JoinGamePage from "./components/JoinGamePage.vue";

const player1 = ref<string | null>(null);
const player2 = ref<string | null>(null);
const playersJoined = ref(false);

const handleJoinGame = (name1: string, name2: string) => {
  player1.value = name1;
  player2.value = name2;
  playersJoined.value = true;
  console.log("handleJoinGame app.vue");
  console.log(player2.value);
};
</script>

<template>
  <div class="site-background">
    <h1 class="neon-text">Tic Tac Toe</h1>
    <div id="app">
      <GameBoard />
    </div>
  </div>
</template>

<style scoped>
.site-background {
  background-color: black;
  color: white; /* Optional: Set a default text color to ensure readability */
  min-height: 100vh; /* Ensure it covers the full viewport height */
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}
.neon-text {
  font-family: "Arial", sans-serif;
  font-size: 3em;
  color: #ff00ff;
  text-shadow: 0 0 5px #ff00ff, 0 0 10px #ff00ff, 0 0 20px #ff00ff,
    0 0 40px #ff00ff, 0 0 80px #ff00ff, 0 0 90px #ff00ff, 0 0 100px #ff00ff,
    0 0 150px #ff00ff;
}
</style>
