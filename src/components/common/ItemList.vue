<template>
  <li v-if="item.name !== 'id'">
    <span>
      <p style="text-align: left">
        <strong>{{
          item.name !== undefined
            ? capitalizeFirst(item.name) + ":"
            : "Имя не задано"
        }}</strong>
      </p>
      <p v-if="!isEditing">
        {{ item.value !== undefined ? item.value : "Номер не задан" }}
      </p>

      <div class="change_field" v-else>
        <button class="edit-btn" @click="acceptСhanges()">&#10004;</button>
        <input type="text" placeholder="New value..." v-model="value" />
        <button class="edit-btn" @click="showModal()">&times;</button>
      </div>
    </span>
    <div class="item-btns">
      <button @click="editBtn()">&#9998;</button>
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
    // изменение регистра
    capitalizeFirst(string) {
      return string.charAt(0).toUpperCase() + string.slice(1);
    },

    // метод изменения поля, если это контакт, то происходит переход на его страницу, если поле с данными, то появляется input для изменения
    editBtn() {
      if (this.type === "contacts") {
        return this.$emit("open-contact", this.item);
      } else {
        this.isEditing = true;
      }
    },

    // метод принятия изменений для выбранных значений
    acceptСhanges() {
      if (this.value.trim()) {
        this.isEditing = false;
        this.item.value = this.value;
        this.value = "";
      }
    },

    // открытие модели для принятия ............................................................... сделать универсальным
    showModal() {
      this.$emit("show-modal", {
        id: this.item.id,
        title: "Отменить изменения?",
        name: this.item.name,
        type: "change",
        callBack: () => this.stopChanging(),
      });
    },

    // прекращение изменений
    stopChanging() {
      this.isEditing = false;
      this.value = "";
    },
  },
};
</script>

<style scoped>
input {
  height: 2rem;
}
button {
  cursor: pointer;
  width: 2rem;
  height: 2rem;
  margin: auto 0;
  border: 0px;
  border-radius: 1rem;
  background-color: tomato;
  color: white;
}
.change_field {
  margin-top: 0.5rem;
  margin-left: 3rem;
  height: 2.4rem;
  display: flex;
  align-content: center;
  justify-content: center;
}
.edit-btn {
  border-radius: 0;
  width: 2rem;
  height: 2.4rem;
}
</style>
