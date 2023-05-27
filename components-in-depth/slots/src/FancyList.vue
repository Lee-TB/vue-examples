<script setup>
import { ref } from 'vue';

const props = defineProps(['api-url', 'per-page']);

const items = ref([]);

// mock remote data fetching
setTimeout(() => {
  items.value = [
    { body: 'Scoped Slots Guide', username: 'Evan You', likes: 20 },
    { body: 'Vue Tutorial', username: 'Natalia Tepluhina', likes: 10 },
  ];
}, 1000);
</script>

<template>
  <ul>
    <li v-if="!items.length">loading...</li>
    <li v-for="item of items">
      <slot name="item" v-bind="item" />
    </li>
  </ul>
</template>
