<template>
  <div>
    <ul>
      <ContactItem 
      v-for="item in items" :key="item.id"
      v-bind:item="item"
      @show-modal='showModal'
      />
      </ul>
      <div v-if="this.isShowing">
        <div class="modal">
          <div class="modal-handler">
            <h3>Удалить контакт?</h3>
            <div class="modal-btns">
              <button @click="isShowing = !isShowing;">Нет</button>
              <button @click="removeContact()">OK</button>
            </div>
          </div>
        </div>
      </div>
  </div>
</template>

<script>
import ContactItem from '@/components/ContactItem'  
export default {
  data() {
    return{
      idRemoved: 0,
      isShowing: false
    }
  },
  props:['items'],
  methods: {
    showModal(id) {
      this.idRemoved = id;
      this.isShowing = !this.isShowing;
      console.log(this.isShowing);
    },
    removeContact() {
      this.isShowing = !this.isShowing;
      this.$emit('remove-contact', this.idRemoved);
    }
  },
  components: {
    ContactItem
  }
}
</script>

<style scoped>
ul {
  list-style: none;
  margin: 0;
  padding: 0;
}
.modal {
  position: fixed;
  top: 0;
  bottom: 0;
  right: 0;
  left: 0;
  background-color: rgba(116, 116, 116, 0.418);
}
.modal-handler {
  width: 20rem;
  position: relative;
  margin: 20rem auto;
  background-color: white;
  padding: 2rem 1rem;
}
.modal-btns {
  width: 8rem;
  display: flex;
  justify-content: space-between;
  margin: auto;
}
</style>