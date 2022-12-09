<script setup>
import SceneBoard from "./GamePage/SceneBoard.vue";
import SceneMenu from "./GamePage/SceneMenu.vue";

const props = defineProps(["app"]);

// eslint-disable-next-line vue/no-mutating-props
props.app.actions = Object.freeze({
  ...props.app.actions,

  startScene() {},

  cleanScene() {
    // eslint-disable-next-line vue/no-mutating-props
    props.app.actions = Object.freeze({
      ...props.app.actions,
      startScene: null,
      cleanScene: null,
    });
  },
});

function finishGame() {
  props.app.actions.goToResult();
}
</script>

<template>
  <SceneBoard :app="props.app" />
  <div
    class="position-absolute h-100 w-100 top-0 d-flex flex-column justify-content-between"
  >
    <div class="text-white d-flex align-items-center">
      <h1 class="text-center flex-fill">HRA</h1>
      <div class="m-2">
        <button @click="app.actions.toggleSceneMenu">MENU</button>
      </div>
    </div>
    <div
      v-if="app.sceneMenuShown"
      class="flex-fill d-flex justify-content-center align-items-center"
    >
      <SceneMenu :app="app" />
    </div>
    <div v-if="!app.sceneMenuShown" class="d-flex justify-content-between">
      <button @click="finishGame">left</button>
      <button>right</button>
    </div>
  </div>
</template>
