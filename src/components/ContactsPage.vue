<template>
  <div>
    <h2 class="title">Contacts</h2>
    <AddFlied @add="addContact" />
    <List
      v-bind:items="items"
      v-bind:type="(type = 'contacts')"
      @remove="removeContact"
      @open-contact="openContact"
    />
  </div>
</template>

<script>
import AddFlied from "@/components/common/AddFlied";
import List from "@/components/common/List";
export default {
  data() {
    return {
      type: "",
    };
  },
  props: ["items"],
  methods: {
    removeContact(info) {
      this.$emit("remove", info);
    },
    addContact(contact) {
      this.$emit("add", contact);
    },
    openContact(item) {
      this.$emit("open-contact", item);
    },
  },
  components: {
    List,
    AddFlied,
  },
};
</script>

<style>
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
  cursor: pointer;
  width: 3rem;
  height: 2.5rem;
  margin: auto 0;
  /* border-radius: 1rem; */
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
