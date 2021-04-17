<template>
  <div>
    <h1 class="title">Contacts</h1>
    <AddContact/>
    <ContactsList
    v-bind:items="items"
    @remove-contact="removeContact"/>
  </div>
</template>

<script>
import AddContact from "@/components/AddContact";
import ContactsList from "@/components/ContactsList";
export default {
  data() {
    return{
      items:[
        {id: 1, name: "Максим Богданец", number: "+79772506127"},
        {id: 2, name: "Мария Белозерова", number: "+79797979797"},
        {id: 3, name: "Костя Физик", number: "+70000000000"},
        {id: 4, name: "Жопа", number: "+жопный номер"}
      ]
    }
  },
  methods: {
    removeContact(id) {
      this.items = this.items.filter(i => i.id != id);
    }
  },
  components: {
    ContactsList, AddContact
  }
}
</script>

<style scoped>
/* .title {} */
</style>