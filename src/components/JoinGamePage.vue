<script setup lang="ts">
import {ref} from 'vue'

const joinGame = () => {
    console.log("Joining the game!");
    
}

const playerName = ref('');
</script>

<template>
    <input type="text" :value="playerName">
    <button @click="joinGame">Join</button>

</template>

<style scoped>
</style>