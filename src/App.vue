<template>
  <div id="app">
    <h1>Phone book</h1>
    <ContactsPage v-if="item === null" @open-contact="openContact" />
    <!-- <ContactPage v-bind:item="item" /> -->
  </div>
</template>

<script>
import ContactsPage from "@/components/ContactsPage";
import ContactPage from "@/components/ContactPage";
export default {
  name: "App",
  data() {
    return {
      item: null,
    };
  },
  methods: {
    openContact(item) {
      console.log(item);
      for (key in item) {
        console.log(key);
        console.log(item[key]);
      }
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
