<script setup>
import { computed } from "vue";

const props = defineProps(["position"]);

const style = computed(() => {
  return {
    top: `${props.position.top}px`,
    left: `${props.position.left}px`,
    height: `${props.position.height}px`,
    width: `${props.position.width}px`,
  };
});
</script>

<template>
  <div class="position-absolute" :style="style">F</div>
</template>
