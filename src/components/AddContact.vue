<template>
  <form>
    <span>
      <input type="text" placeholder="Enter name..."> 
      <input type="text" placeholder="Enter phone number...">
    
    <button type="submit">ADD</button>
    </span>
  </form>
</template>

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