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
    <header class="header">
      <h1 class="neon-text">Tic Tac Toe</h1>
    </header>
    <div id="app">
      <GameBoard />
    </div>
  </div>
</template>

<style scoped>
.site-background {
  background: linear-gradient(135deg, #000, #111);
  color: white;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}
.header {
  text-align: center;
  padding: 1em;
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
