<template>
  <div>
    <ul>
      <Itemlist
        v-for="value in items"
        :key="value.id"
        v-bind:item="value"
        @show-modal="showModal"
        @open-contact="openContact"
      />
    </ul>

    <div v-if="isShowing" class="modal">
      <div class="modal-handler">
        <h3 id="modal-title" v-html="modal_title"></h3>
        <div class="modal-btns">
          <button @click="removeContact()">OK</button>
          <button @click="closeModal()">Нет</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Itemlist from "@/components/common/ItemList";
export default {
  data() {
    return {
      modal_title: "Удалить контакт?",
      info: {},
      isShowing: false,
    };
  },
  props: {
    items: {
      required: true,
    },
    type: {
      type: String,
    },
  },
  methods: {
    showModal(info) {
      this.info = info;
      this.modal_title = info.title;
      this.isShowing = true;
    },
    closeModal() {
      this.isShowing = false;
    },
    removeContact() {
      this.isShowing = false;
      this.$emit("remove", this.info);
    },
    openContact(item) {
      this.$emit("open-contact", item);
    },
  },
  components: {
    Itemlist,
  },
};
</script>

<style scoped>
ul {
  list-style: none;
  margin: 0;
  padding: 0;
}
button {
  cursor: pointer;
  margin: auto 0;
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
  border: 1px solid black;
  padding: 2rem 1rem;
}
.modal-btns {
  width: 8rem;
  display: flex;
  justify-content: space-between;
  margin: auto;
}
</style>
