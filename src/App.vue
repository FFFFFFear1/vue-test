<template>
  <div id="app">
    <ContactsPage/>
  </div>
</template>

<script>
import ContactsPage from "@/components/ContactsPage"
export default {
  name: 'App',
  components: {
    ContactsPage
  }
}
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
