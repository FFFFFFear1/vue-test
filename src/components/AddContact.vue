<template>
  <form @submit.prevent="addNewContact">
    <span>
      <input type="text" placeholder="Enter name..." v-model="name"> 
      <input type="text" placeholder="Enter phone number..." v-model="number">
      <button type="submit">ADD</button>
    </span>
  </form>
</template>

<script >
export default {
  data() {
    return{
      name: '',
      number:''
    }
  },
  methods: {
    addNewContact() {
      if(this.name.trim() && this.number.trim()) {
        const contact = {
          id: Date.now(),
          name: this.name,
          number: this.number
        }
        console.log(contact.id);
        this.$emit('add-contact', contact);
        this.name = '';
        this.number ='';
      }
    }
  }
}
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