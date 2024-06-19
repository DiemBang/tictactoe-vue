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
  <h1>Tic Tac Toe</h1>
  <div id="app">
    <GameBoard />
  </div>
</template>

<style scoped></style>
