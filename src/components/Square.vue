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
    {{ value }}
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
</style>
