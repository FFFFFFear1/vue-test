<template>
  <form @submit.prevent="addNewField" class="guide">
    <span>
      <!-- выплывающий список типов полей, виден только когда открыт контакт -->
      <select v-if="type === 'contact'" v-model="name">
        <option value="" disabled selected>Выберите значение из списка</option>
        <option
          aria-placeholder="dsdsd"
          v-for="field in fields"
          :key="field.index"
          :value="field"
        >
          {{ capitalizeFirst(field) }}
        </option>
      </select>

      <!-- вводной поле для имени, виден только когда открыт контакты -->
      <input
        v-else
        type="text"
        maxlength="30"
        minlength="3"
        pattern="^[A-Za-zА-Яа-яЁё]+$"
        placeholder="Enter name..."
        required
        v-model="name"
      />

      <!-- поле для ввода значения -->
      <input
        type="text"
        maxlength="30"
        minlength="1"
        placeholder="Enter value..."
        required
        v-model="value"
      />
      <button type="submit">ADD</button>
    </span>
  </form>
</template>

<script type="text/x-template" id="anchored-heading-template">
export default {
  name: "guide",
  data() {
    return {
      name: "",
      value: "",
      fields: ["name",'number','email','age', 'status','other'],
    };
  },
  props: {
    item: {
      type: Array,
    },
    type: {
      type: String,
      required: true
    },
  },
  methods: {
    // изменение регистра
    capitalizeFirst(string) {
      return string.charAt(0).toUpperCase() + string.slice(1);
    },

    // добавление нового поля, подходит для любого листа
    addNewField() {
      if (this.name.trim() && this.value.trim()) {
        const field = {
          id: Date.now(),
          name: this.name,
          value: this.value,
        };
        this.$emit("add", field);
        this.name = "";
        this.value = "";
      }
    },
  },
};
</script>

<style scoped>
form {
  margin: 2rem;
}
button {
  font-weight: bold;
  background-color: tomato;
  color: white;
}
span {
  margin: auto;
  width: 40rem;
  display: grid;
  grid-template-columns: 45% 45% 10%;
  border: 2px solid rgb(255, 255, 255);
}
input {
  border: 0px;
  padding: 0.5rem;
}
</style>
