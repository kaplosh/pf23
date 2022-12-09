<script setup>
import { onMounted, onUnmounted, reactive, ref } from "vue";
import UserFigure from "./UserFigure.vue";

const boardRef = ref(null);
const resizeObserver = ref(null);

const BOARD_LIMIT = 1000;
const SCENE_SIZE_RATIO = BOARD_LIMIT / 690; // w = h / r  |  h = w * r

const scene = reactive({
  height: BOARD_LIMIT,
  width: BOARD_LIMIT / SCENE_SIZE_RATIO,
});

const FIGURE_DIMENSIONS = [210, 120];
const userFigurePosition = reactive({
  top: scene.height - FIGURE_DIMENSIONS[0] - 120,
  left: scene.width / 2 - FIGURE_DIMENSIONS[1] / 2,
  height: FIGURE_DIMENSIONS[0],
  width: FIGURE_DIMENSIONS[1],
});

function recomputeSceneSize(maxHeight, maxWidth) {
  const previousSceneHeight = scene.height;

  scene.height = maxHeight > BOARD_LIMIT ? BOARD_LIMIT : maxHeight;
  scene.width = scene.height / SCENE_SIZE_RATIO;
  if (scene.width > maxWidth) {
    scene.width = maxWidth;
    scene.height = scene.width * SCENE_SIZE_RATIO;
  }

  const changeRatio = scene.height / previousSceneHeight;
  const sizeRatio = scene.height / BOARD_LIMIT;

  userFigurePosition.top *= changeRatio;
  userFigurePosition.left *= changeRatio;
  userFigurePosition.height = sizeRatio * FIGURE_DIMENSIONS[0];
  userFigurePosition.width = sizeRatio * FIGURE_DIMENSIONS[1];
}

onMounted(() => {
  resizeObserver.value = new ResizeObserver((entries) => {
    for (const entry of entries) {
      // Firefox implements `contentBoxSize` as a single content rect, rather than an array
      const contentBoxSize = Array.isArray(entry.contentBoxSize)
        ? entry.contentBoxSize?.[0]
        : entry.contentBoxSize;
      if (contentBoxSize) {
        recomputeSceneSize(contentBoxSize.blockSize, contentBoxSize.inlineSize);
      }
    }
  });

  resizeObserver.value.observe(boardRef.value);
  recomputeSceneSize(boardRef.value.clientHeight, boardRef.value.clientWidth);
});

onUnmounted(() => {
  if (boardRef.value) resizeObserver.value?.unobserve(boardRef.value);
});
</script>

<template>
  <div
    ref="boardRef"
    class="h-100 w-100 overflow-hidden bg-black d-flex justify-content-center align-items-center"
  >
    <div
      :style="{
        height: `${scene.height}px`,
        width: `${scene.width}px`,
      }"
      class="bg-light bg-opacity-25 position-relative"
    >
      <UserFigure :position="userFigurePosition" class="bg-info" />
    </div>
  </div>
</template>
