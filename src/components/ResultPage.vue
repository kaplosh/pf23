<script setup>
const props = defineProps(["app"]);
</script>

<template>
  <div>
    <h1 class="text-white">result</h1>
    <br />
    <button @click="props.app.actions.goToHome">zacni znovu</button>
  </div>
</template>
