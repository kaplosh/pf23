<script setup>
import { reactive } from "vue";
import HomePage from "./components/HomePage.vue";
import GamePage from "./components/GamePage.vue";
import ResultPage from "./components/ResultPage.vue";

const app = reactive({
  currentPage: "home",
  sceneMenuShown: false,
  playerName: "",
  result: {
    values: {
      sym1: 0,
      sym2: 0,
      sym3: 0,
      sym4: 0,
    },
    //text: "not-clean",
  },

  actions: Object.freeze({
    startNewGame() {
      app.currentPage = "game";
      app.actions.startScene?.();
    },

    cleanResult() {
      app.result.text = "clean";
    },

    goToHome() {
      app.currentPage = "home";
      app.actions.cleanResult();
      app.actions.cleanScene?.();
    },

    goToResult() {
      app.currentPage = "result";
      app.actions.cleanScene?.();
    },

    toggleSceneMenu() {
      app.sceneMenuShown = !app.sceneMenuShown;
    },

    startScene: null, // is set by SceneBoard
    cleanScene: null, // is set by SceneBoard
  }),
});
</script>

<template>
  <div class="bg-black h-100 position-relative">
    <HomePage v-if="app.currentPage === 'home'" :app="app" />
    <GamePage v-if="app.currentPage === 'game'" :app="app" />
    <ResultPage v-if="app.currentPage === 'result'" :app="app" />
  </div>
</template>
