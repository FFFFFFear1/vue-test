<template>
  <li v-if="item.name !== 'id'">
    <span>
      <p style="text-align: left">
        <strong>{{ item.name !== undefined ? item.name : "нет имени" }}</strong>
      </p>
      <p v-if="!isEditing">
        {{ item.value !== undefined ? item.value : "нет номера" }}
      </p>

      <div class="change_field" v-else>
        <button @click="edit()">&#10004;</button>
        <input type="text" placeholder="New value..." v-model="value" />
        <button @click="showModal()">&times;</button>
      </div>
    </span>
    <div class="item-btns">
      <button @click="callBack()">&#9998;</button>
      <button
        @click="
          $emit('show-modal', {
            id: item.id,
            title: 'Удалить ' + item.name + '?',
            name: item.name,
            type: 'delete',
          })
        "
      >
        &times;
      </button>
    </div>
  </li>
</template>

<script>
export default {
  data() {
    return {
      value: "",
      isEditing: false,
    };
  },
  props: {
    item: {
      type: Object,
      required: true,
    },
    type: {
      type: String,
    },
  },
  methods: {
    callBack() {
      if (this.type === "contacts") {
        return this.$emit("open-contact", this.item);
      } else {
        this.isEditing = true;
      }
    },
    stopChanging() {
      this.isEditing = false;
      this.value = "";
    },
    showModal() {
      this.$emit("show-modal", {
        id: this.item.id,
        title: "Отменить изменения?",
        name: this.item.name,
        type: "change",
        callBack: () => this.stopChanging(),
      });
    },
    edit() {
      // ДОБАВИТЬ ВЫЗОВ МОДЕЛИ КАК ПРИ УДАЛЕНИИ
      // ПОДУМАТЬ КАК СДЕЛАТЬ ЕЕ УНИВЕРСАЛЬНОЙ

      if (this.value.trim()) {
        this.isEditing = false;
        this.item.value = this.value;
        this.value = "";
      }
    },
  },
};
</script>

<style scoped>
input {
  height: 2rem;
}
.change_field {
  margin-top: 0.5rem;
  margin-left: 3rem;
  height: 2.4rem;
  display: flex;
  align-content: center;
  justify-content: center;
}
</style>
