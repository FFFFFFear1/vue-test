<template>
  <form @submit.prevent="addNewField">
    <span>
      <input type="text" placeholder="Enter name..." v-model="name" />
      <input type="text" placeholder="Enter value..." v-model="value" />
      <button type="submit">ADD</button>
    </span>
  </form>
</template>

<script>
export default {
  data() {
    return {
      name: "",
      value: "",
    };
  },
  methods: {
    addNewField() {
      if (this.name.trim() && this.value.trim()) {
        const field = {
          id: Date.now(),
          name: this.name,
          value: this.value,
        };
        this.$emit("add", field);
        this.name = "";
        this.value = "";
      }
    },
  },
};
</script>

<style scoped>
form {
  margin: 2rem;
}
span {
  margin: auto;
  width: 40rem;
  display: grid;
  grid-template-columns: 45% 45% 10%;
}
input {
  padding: 0.5rem;
}
</style>
