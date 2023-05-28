<script setup>
import { ref, provide } from 'vue';
import Child from './Child.vue';
import LocationProvider from './LocationProvider.vue';

const message = ref('hello from app');
provide('msg', message);
</script>

<template>
  <h2>Simple example</h2>
  <input type="text" v-model="message" />
  <Child />

  <h2>Working with Reactivity</h2>
  <LocationProvider />
</template>
