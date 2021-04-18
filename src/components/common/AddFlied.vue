<template>
  <form @submit.prevent="addNewField" class="guide">
    <span>
      <select v-if="type === 'contact'" v-model="name">
        <option v-for="field in fields" :key="field.index" :value="field">
          {{ field }}
        </option>
      </select>

      <input v-else type="text" placeholder="Enter name..." v-model="name" />
      <input type="text" placeholder="Enter value..." v-model="value" />
      <button type="submit">ADD</button>
    </span>
  </form>
</template>

<script type="text/x-template" id="anchored-heading-template">
export default {
  name: "guide",
  data() {
    return {
      name: "",
      value: "",
      fields: ["name",'number','email','age', 'status','other'],
    };
  },
  props: {
    item: {
      type: Array,
    },
    type: {
      type: String,
    },
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
