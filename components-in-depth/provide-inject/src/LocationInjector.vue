<script setup>
import { inject } from 'vue';

const { location, updateLocation } = inject('location');
const count = inject('read-only-count');
</script>

<template>
  <h3>Location</h3>
  <button @click="updateLocation">
    {{ location }}
  </button>
  <h3>Read only count</h3>
  <button @click="count++">{{ count }}</button>
</template>
