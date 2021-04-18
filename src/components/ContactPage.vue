<template>
  <div>
    <h2 class="description">Contact</h2>
    <AddFlied
      v-bind:item="item"
      v-bind:type="(type = 'contact')"
      @add="addField"
    />
    <List
      v-bind:items="item"
      v-bind:type="(type = 'contact')"
      @remove="removeField"
    />
    <!-- <button @click="$emit('back')">cancel</button> -->
    <button class="exit-btn" @click="$emit('back')">Go back</button>
    <!-- v-on:open-contact="openContact"/> -->
  </div>
</template>

<script>
import AddFlied from "@/components/common/AddFlied";
import List from "@/components/common/List";

export default {
  data() {
    return {
      type: "",
    };
  },
  props: {
    item: {
      required: true,
    },
  },
  methods: {
    // передача команды удаления поля в App
    removeField(info) {
      this.$emit("remove", info);
    },

    // передача команды добавления поля в App
    addField(field) {
      this.$emit("add", field);
    },
  },
  components: {
    List,
    AddFlied,
  },
};
</script>

<style scoped>
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
.exit-btn {
  margin-top: 2rem;
  padding: 12px;
  width: 8rem;
  border: 1px solid white;
  font-weight: bold;
  background-color: tomato;
  color: white;
}
</style>
