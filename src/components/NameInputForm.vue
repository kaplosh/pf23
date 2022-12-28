<script>
const bannedNames = ["anna", "petra"];

export default {
  data() {
    return {
      errorMSg: null,
    };
  },

  methods: {
    onInput(event) {
      const name = event.target.value.trim();
      if (bannedNames.includes(name.toLowerCase())) {
        this.errorMSg = "Tohle není validní jméno..";
        this.$emit("set", "");
      } else {
        this.errorMSg = null;
        this.$emit("set", name);
      }
    },
  },
};
</script>

<template>
  <div class="form-outline form-white">
    <input @input="onInput" placeholder="Napiš své jméno.." />
    <div v-if="errorMSg !== null">{{ errorMSg }}</div>
  </div>
</template>
