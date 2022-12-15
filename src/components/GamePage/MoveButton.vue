<script setup>
import { onUnmounted } from "vue";

const emit = defineEmits(["change"]);

onUnmounted(() => {
  emit("change", false);
});
</script>

<template>
  <button onmousedown="emit('change', true)" onmouseup="emit('change', false)">
    <slot />
  </button>
</template>
