<script>
import NameInputForm from "./NameInputForm.vue";

export default {
  components: {
    NameInputForm,
  },

  props: ["app"],

  methods: {
    onNameChange(name) {
      // eslint-disable-next-line vue/no-mutating-props
      this.app.playerName = name;
    },
    onClick() {
      if (this.app.playerName) {
        this.app.actions.startNewGame();
      }
    },
  },
};
//posílání props mezi komponentami
</script>

<template>
  <div class="position-absolute top-50 start-50 translate-middle">
    <h1 class="text-white position-absolute start-50 translate-middle">
      Vítej
    </h1>
    <br />
    <NameInputForm :name="app.playerName" @set="onNameChange" />
    <br />
    <button
      class="btn btn-outline-success position-absolute start-100 translate-middle mt-2"
      @click="onClick"
    >
      zacni
    </button>
  </div>
</template>
