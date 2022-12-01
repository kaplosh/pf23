<script>
const bannedNames = ["anna", "petra"];

export default {
  data() {
    return {
      nameInput: "",
      errorMSg: null,
    };
  },

  methods: {
    createPlayer() {
      const name = this.nameInput.trim();
      //console.log(name.toLowerCase());
      if (bannedNames.includes(name.toLowerCase())) {
        this.errorMSg = "Tohle není validní jméno..";
      } else {
        this.errorMSg = null;
        this.$emit("select", name);
      }
    },
  },
};
</script>

<template>
  <div>
    <h3>Negře</h3>
    <input v-model="nameInput" placeholder="Napiš své jméno.." />
    <button @click="createPlayer">Vytvoř se</button>
    <div v-if="errorMSg !== null">{{ errorMSg }}</div>
  </div>
</template>
