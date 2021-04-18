<template>
  <div>
    <ul>
      <Itemlist
        v-for="value in items"
        :key="value.id"
        v-bind:item="value"
        v-bind:type="type"
        @show-modal="showModal"
        @open-contact="openContact"
      />
    </ul>

    <!-- модель для принятия изменения -->
    <div v-if="isShowing" class="modal">
      <div class="modal-handler">
        <h3 id="modal-title" v-html="modal_title"></h3>
        <div class="modal-btns">
          <button id="apply-btn" @click="removeContact()">OK</button>
          <button id="cancel-btn" @click="closeModal()">Нет</button>
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
    // показ модели
    showModal(info) {
      this.isShowing = true;
      this.modal_title = info.title;
      this.info = info;
    },

    // закрытие модели
    closeModal() {
      this.isShowing = false;
    },

    // передача команды удаления контакта в App
    removeContact() {
      this.closeModal();
      if (this.info.type === "delete") {
        this.$emit("remove", this.info);
      } else {
        this.info.callBack();
      }
    },

    // передача команды открытия контакта в App
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
  border: 0px;
  font-weight: bold;
  padding: 0.5rem 1rem;
  background-color: tomato;
  color: white;
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
  border: 1px solid rgb(255, 128, 128);
  padding: 2rem 1rem;
}
.modal-btns {
  width: 8rem;
  display: flex;
  justify-content: space-between;
  margin: auto;
}
</style>
