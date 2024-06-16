<script setup lang="ts">
import { ref } from "vue";

const username = ref("");

const handleUsernameInput = (e: Event) => {
  const target = e.target as HTMLInputElement;
  username.value = target.value;
};

const handleJoinGame = () => {
  console.log("Player Name:", username.value);

  // Save to local storage
  localStorage.setItem("playerName", username.value);
  emit('joinGame', username.value);
};

const emit = defineEmits<{ (event: 'joinGame', name: string): void }>();
</script>

<template>
  <div id="playerInput">
    <h2>Enter your name to join the game</h2>

    <form @submit.prevent="handleJoinGame">
      <div>
        
        <input
          type="text"
          id="username"
          v-model="username"
          @input="handleUsernameInput"
          placeholder="Your name"
        />

        <button type="submit" @click.prevent="handleJoinGame">Join game</button>
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
