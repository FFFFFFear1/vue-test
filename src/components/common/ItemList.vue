<template>
  <li>
    <span>
      <p style="text-align: left">
        <strong>{{ item.name }}</strong>
      </p>
      <p>{{ item.value }}</p>
    </span>
    <div class="item-btns">
      <button @click="$emit('open-contact', item)">&#9998;</button>
      <button
        @click="
          $emit('show-modal', {
            id: item.id,
            title: 'Удалить ' + item.name + '?',
            name: item.name,
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
  props: {
    item: {
      type: Object,
      required: true,
    },
  },
  methods: {},
};
</script>
