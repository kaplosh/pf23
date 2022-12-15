<script>
import NameInputForm from "./NameInputForm.vue";

export default {
  components: {
    NameInputForm,
  },
  data() {
    return {
      isMenuOpened: false,
    };
  },

  methods: {
    onBegin(name) {
      console.log(name);
    },
    onOpenMenu() {
      this.isMenuOpened = true;
    },
  },
};
</script>

<template>
  <div class="page position-relative bg-secondary">
    <div class="d-flex justify-content-end p-2">
      <button @click="onOpenMenu" class="btn btn-outline-primary">
        <i class="bi bi-list" />
      </button>
    </div>
    <div
      class="position-absolute w-100 h-100 top-0 start-0 d-flex justify-content-center align-items-center"
      @click="isMenuOpened = false"
      v-if="isMenuOpened"
    >
      <div class="shadow rounded bg-body">Text menu</div>
    </div>
  </div>
</template>
