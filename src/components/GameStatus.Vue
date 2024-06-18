<script setup lang="ts">
const props = defineProps<{ status: string }>();
</script>

<template>
  <div class="status">
    {{ status }}
  </div>
</template>

<style scoped>
.status {
  margin-bottom: 10px;
  font-size: 1.5em;
  text-align: center;
}
</style>
