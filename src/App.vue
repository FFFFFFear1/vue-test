<template>
  <div id="app">
    <h1>Phone book</h1>
    <ContactsPage
      v-if="item.length === 0"
      v-bind:items="items"
      @open-contact="openContact"
      @remove="removeContact"
      @add="addContact"
    />
    <ContactPage
      v-else
      v-bind:item="item"
      @remove="removeField"
      @add="addField"
      @back="closeContact"
    />
  </div>
</template>

<script>
import Vue from "vue";
import ContactsPage from "@/components/ContactsPage";
import ContactPage from "@/components/ContactPage";

var vm = new Vue({
  data: {
    item: [],
    items: [
      { id: 1, name: "Максим Богданец", value: "+79772506127" },
      { id: 2, name: "Мария Белозерова", value: "+79797979797" },
      { id: 3, name: "Костя Физик", value: "+70000000000" },
      { id: 4, name: "Никита Федотов", value: "+123123123" },
    ],
  },
});

export default {
  name: "App",
  data() {
    return {
      item: vm.item,
      items: vm.items,
    };
  },
  methods: {
    openContact(item) {
      for (var key in item) {
        if (key === "value") {
          this.item.push({
            name: "number",
            value: item[key] !== undefined ? item[key] : "",
          });
        } else {
          this.item.push({
            name: key !== undefined ? key : "",
            value: item[key] !== undefined ? item[key] : "",
          });
        }
      }
    },
    closeContact() {
      let newItem = {};
      for (var key in this.item) {
        newItem[
          this.item[key].name === "number" ? "value" : this.item[key].name
        ] = this.item[key].value;
      }
      this.items = this.items.filter((i) => i.id != newItem.id);
      this.items.push(newItem);
      this.item.splice(0, this.item.length);
    },
    removeContact(info) {
      this.items = this.items.filter((i) => i.id != info.id);
    },
    addContact(contact) {
      this.items.push(contact);
    },
    removeField(info) {
      this.item = this.item.filter((i) => i.name != info.name);
    },
    addField(field) {
      this.item = this.item.filter((i) => i.name != field.name);
      this.item.push({ name: field.name, value: field.value });
    },
  },
  components: {
    ContactsPage,
    ContactPage,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
