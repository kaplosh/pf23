<script setup>
const props = defineProps(["app"]);

const resultMessage = computed(() => {
  // props.app.values.sym1 (number)
  // prvni vreta = ceho je nejvice,
  // druha veta ceho je nejmine
  const result = 'neco';
  return result;
});
</script>

<template>
  <div class="position-absolute top-50 start-50 translate-middle">
    <h1 class="text-white">result</h1>
    <div>
      {{ app.playerName }}
      <br />
      {{ resultMessage }}
    </div>
    <br />
    <button class="btn btn-outline-light" @click="props.app.actions.goToHome">
      zacni znovu
    </button>
  </div>
</template>
