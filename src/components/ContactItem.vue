<template>
    <li>
        <span>
            <p style="text-align: left"><strong>{{item.name}}</strong></p>
            <p>{{item.number}}</p>
        </span>
        <button @click="$emit('show-modal', item.id)">&times;</button>  
        <!-- <button @click="$emit('remove-contact', item.id)">&times;</button>   -->
    </li>
</template>

<script>
export default {
  props: {
    item: {
      type: Object,
      required: true
    }
  },
}

</script>

<style scoped>
li {
    cursor: pointer;
    display: flex;
    justify-content: space-between;
    margin: 1rem auto;
    width: 40rem;
    padding: 0.5rem 2rem;
    border: 1px solid black;
    border-radius: 1rem;
}
button{
  height: 1.8rem;
  margin: auto 0;
  border-radius: 1rem;
}
span {
    width: 30rem;
    display: grid;
    grid-template-columns: 50% 50%;
    text-align: center;
}
</style>