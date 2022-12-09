<script setup>
const props = defineProps(["app"]);

function giveUp() {
  props.app.actions.toggleSceneMenu();
  props.app.actions.goToHome();
}
</script>

<template>
  <div class="bg-light m-4" :style="{ maxWidth: '400px' }">
    <h2>pause</h2>
    <button @click="props.app.actions.toggleSceneMenu">Continue</button>
    <br />
    <button @click="giveUp">Give Up</button>
  </div>
</template>
