<script setup lang="ts">

const props = defineProps<{ value: string | null }>();
const emit = defineEmits<{ (event: "click"): void }>();

const handleClick = () => {
  if (!props.value) {
    emit("click");
  }
};
</script>

<template>
   <div class="square" @click="handleClick">
    <span v-if="value" :class="['neon', value === 'X' ? 'x' : 'o']">{{ value }}</span>
  </div>
</template>

<style scoped>
.square {
  width: 100px;
  height: 100px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 2em;
  border: 1px solid #000;
  cursor: pointer;
}

.neon {
  font-family: 'Arial', sans-serif;
  color: #007bff;
  text-shadow: 
    0 0 5px #007bff,
    0 0 10px #007bff,
    0 0 20px #007bff,
    0 0 40px #007bff,
    0 0 80px #007bff;
}
</style>
