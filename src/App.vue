<template>
  <div id="app">
    <h1 class="title">Phone book</h1>
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
      { id: 1, name: "Bogdanec Maxim", value: "+7912341234" },
      { id: 2, name: "Belozerova Maria", value: "+7909870897" },
      { id: 3, name: "Fizick", value: "+7434343323" },
      { id: 4, name: "Fedotov Nikita", value: "+5565656556" },
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
    // открытие контакта
    openContact(item) {
      for (var key in item) {
        this.item.push({
          name: key === "value" ? "number" : key !== undefined ? key : "",
          value: item[key] !== undefined ? item[key] : "",
        });
      }
    },

    // закрытие контакта
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

    // удаление контакта
    removeContact(info) {
      this.items = this.items.filter((i) => i.id != info.id);
    },

    // добавление контакта
    addContact(contact) {
      this.items.push(contact);
    },

    // удаление поля
    removeField(info) {
      this.item = this.item.filter((i) => i.name != info.name);
    },

    // добавление поля
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
body {
  background-color: #38a10e9d;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: auto;
  margin-top: 60px;
  padding: 3rem;
  background-color: #ffa048;
  width: 50rem;
  border: 1px solid rgb(255, 105, 36);
  border-radius: 2rem;
}
li {
  display: flex;
  justify-content: space-between;
  margin: 1rem auto;
  width: 40rem;
  padding: 0.5rem 2rem;
  border: 1px solid rgb(255, 179, 179);
  background-color: rgb(255, 255, 255);
  border-radius: 1rem;
}
.title {
  font-size: 40px;
  color: white;
}
.description {
  font-size: 30px;
  color: white;
}
</style>
