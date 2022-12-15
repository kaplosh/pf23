<script>
import NameInputForm from "./NameInputForm.vue";

export default {
  components: {
    NameInputForm,
  },
  data() {
    return {};
  },

  methods: {
    onBegin (name) {
        console.log(name);
    }
  },
};
</script>

<template>
  <div class="page">
    <name-input-form @select="onBegin" />
  </div>
</template>
