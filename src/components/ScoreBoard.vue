<script setup lang="ts">
const props = defineProps({
  player1: String,
  player2: String,
  player1Score: Number,
  player2Score: Number,
});
</script>

<template>
  <h3>Scoreboard</h3>
  <div class="scoreboard">
    <div>{{ player1 }}: {{ player1Score }}</div>
    <div>{{ player2 }}: {{ player2Score }}</div>
  </div>
</template>

<style scoped>
.scoreboard {
  margin-bottom: 1em;
  display: flex;
  justify-content: space-around;
  font-size: 1.2em;
}
</style>
