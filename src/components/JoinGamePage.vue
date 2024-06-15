<script setup lang="ts">
import { ref } from "vue";

const username = ref<string>("");

const handleUsernameInput = (e: Event) => {
  const target = e.target as HTMLInputElement;
  username.value = target.value;
};

const handleJoinGame = () => {
  console.log("Player Name:", username.value);
  
  // Save to local storage
  localStorage.setItem('playerName', username.value);
};

</script>

<template>
  <form @submit.prevent="handleJoinGame">
    <div id="join-game">
      <label for="username">Enter your name:</label>
      <input
        type="text"
        id="username"
        v-model="username"
        @input="handleUsernameInput"
        placeholder="Your name"
      />

      <button type="submit" @click.prevent="handleJoinGame">Join</button>
    </div>
  </form>
</template>

<style scoped>
#join-game {
  max-width: 400px;
  margin: auto;
  padding: 1em;
  border: 1px solid #ccc;
  border-radius: 4px;
}

#join-game div {
  margin-bottom: 1em;
}

#join-game label {
  display: block;
  margin-bottom: 0.5em;
}

#join-game input {
  width: 100%;
  padding: 0.5em;
  box-sizing: border-box;
}

#join-game button {
  width: 100%;
  padding: 0.5em;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

#join-game button:hover {
  background-color: #0056b3;
}
</style>
