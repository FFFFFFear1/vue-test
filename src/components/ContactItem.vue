<template>
    <li>
        <span>
            <p style="text-align: left"><strong>{{item.name}}</strong></p>
            <p>{{item.number}}</p>
        </span>  
        <div class="item-btns">
          <button @click="print()">&#9998;</button>  
          <button v-on:click="$emit('show-modal', item.id)">&times;</button>
        </div>
        <!-- <button @click="$emit('remove-contact', item.id)"> &times;</button>   -->
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
  methods: {
    print() {
      console.log(item);
    }
  },
}

</script>

<style scoped>
li {
  display: flex;
  justify-content: space-between;
  margin: 1rem auto;
  width: 40rem;
  padding: 0.5rem 2rem;
  border: 1px solid black;
  border-radius: 1rem;
}
button{
  cursor: pointer;
  width: 2rem;
  height: 2rem;
  margin: auto 0;
  border-radius: 1rem;
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