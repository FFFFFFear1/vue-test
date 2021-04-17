<template>
  <div>
    <h2 class="title">Contact</h2>
    <AddFlied @add="addField" />
    <List
      v-bind:items="item"
      v-bind:type="(type = 'contact')"
      @remove="removeField"
    />
    <!-- v-on:open-contact="openContact"/> -->
  </div>
</template>

<script>
import AddFlied from "@/components/common/AddFlied";
import List from "@/components/common/List";

export default {
  data() {
    return {
      item: this.item,
      type: "",
    };
  },
  props: {
    item: {
      required: true,
    },
  },
  methods: {
    removeField(info) {
      this.item = this.item.filter((i) => i.name != info.name);
    },
    addField(field) {
      this.item.push({ name: field.name, value: field.value });
    },
  },
  components: {
    List,
    AddFlied,
  },
};
</script>

<style scoped>
li {
  display: flex;
  justify-content: space-between;
  margin: 1rem auto;
  width: 40rem;
  padding: 0.5rem 2rem;
  border: 1px solid black;
  border-radius: 1rem;
}
button {
  /* cursor: pointer;
  width: 2rem;
  height: 2rem;
  margin: auto 0;
  border-radius: 1rem; */
}
span {
  width: 30rem;
  display: grid;
  grid-template-columns: 50% 50%;
  text-align: center;
}
.item-btns {
  width: 5rem;
  display: flex;
  justify-content: space-between;
}
</style>
