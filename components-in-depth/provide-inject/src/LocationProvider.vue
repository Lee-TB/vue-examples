<script setup>
import { ref, provide, readonly } from 'vue';
import LocationBetween from './LocationBetween.vue';
// Keep any mutations inside of the provider
const location = ref('Sai Gon');
function updateLocation() {
  location.value = location.value === 'Sai Gon' ? 'Ha Noi' : 'Sai Gon';
}
provide('location', { location, updateLocation });

// Wrap the provided value with readonly()
// to ensure the data cannot be mutated by the injector component
const count = ref(0);
provide('read-only-count', readonly(count)); // remove readonly() and try again to see the difference
</script>

<template>
  <LocationBetween />
</template>
