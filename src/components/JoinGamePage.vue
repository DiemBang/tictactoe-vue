<script setup lang="ts">
import { ref } from "vue";

const player1 = ref("");
const player2 = ref("");

const step = ref(1);

const handleJoinGame = () => {
  if (step.value === 1) {
    localStorage.setItem("player1Name", player1.value);
    step.value = 2;
  } else if (step.value === 2) {
    localStorage.setItem("player2Name", player2.value);
    emit("joinGame", player1.value, player2.value);
  }
};

const emit = defineEmits<{
  (event: "joinGame", player1: string, player2: string): void;
}>();
</script>

<template>
  <div id="playerInput">
    <h2 v-if="step === 1">Enter Player 1's name</h2>
    <h2 v-if="step === 2">Enter Player 2's name</h2>

    <form @submit.prevent="handleJoinGame">
        <div v-if="step === 1">
        
        <input
          type="text"
          id="player1"
          v-model="player1"
          placeholder="Player 1's name"
        />
      </div>
      <div v-if="step === 2">
        
        <input
          type="text"
          id="player2"
          v-model="player2"
          placeholder="Player 2's name"
        />
      </div>
      <div>
        <button v-if="step === 1" type="submit">Next</button>
        <button v-else="step === 2" type="submit">Join game</button>
      </div>
    </form>
  </div>
</template>

<style scoped>
#playerInput {
  max-width: 400px;
  margin: auto;
  padding: 1em;
 
}

#playerInput div {
  margin-bottom: 1em;
}

#playerInput label {
  display: block;
  margin-bottom: 0.5em;
}

#playerInput input {
  width: 100%;
  padding: 0.5em;
  box-sizing: border-box;
}

#playerInput button {
  width: 100%;
  padding: 0.5em;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

#playerInput button:hover {
  background-color: #0056b3;
}
</style>
