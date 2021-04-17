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
      items: [
        { id: 1, name: "Максим Богданец", value: "+79772506127" },
        { id: 2, name: "Мария Белозерова", value: "+79797979797" },
        { id: 3, name: "Костя Физик", value: "+70000000000" },
        { id: 4, name: "Никита Федотов", value: "+123123123" },
      ],
    };
  },
  methods: {
    removeContact(info) {
      this.items = this.items.filter((i) => i.id != info.id);
    },
    addContact(contact) {
      this.items.push(contact);
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
