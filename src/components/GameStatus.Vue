<script setup lang="ts">
const props = defineProps<{ status: string }>();
</script>

<template>
  <div class="status-message">
    {{ status }}
  </div>
</template>

<style scoped>
.status-message {
  font-family: 'Orbitron', sans-serif;
  color: #00ff00; 
  background-color: #333; 
  padding: 15px;
  border-radius: 8px;
  text-align: center;
  margin: 10px 0;
  border: 2px solid #00ff00; 
  font-size: 1.2em; 
  letter-spacing: 2px; 
}
</style>
